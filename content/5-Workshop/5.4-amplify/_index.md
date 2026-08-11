---
title: "REST API & User Authentication (Cognito, API Gateway & Lambda API)"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---
### 5.4 REST API Construction & User Authentication (Cognito, API Gateway & Lambda API)

#### 5.4.1. Security Architecture and API Routing

The system establishes a secure communication gateway for the frontend application using a RESTful API architecture. User identity is managed via Cognito User Pools. All incoming requests pass through the AWS WAF firewall before API Gateway validates the JWT token and forwards the request to the Lambda Backend.

#### 5.4.2. Detailed Table of Endpoints and Backend Services
| HTTP Method  | API Endpoint   | Lambda API Execution Function  | Connected AWS Service |
| :--- | :--- | :--- | :--- |
| **POST** | */auth/login* | Authenticates user credentials and returns a JWT Token | Amazon Cognito |
| **GET** | */financials/{ticker}* | Queries the financial indicator matrix for a ticker symbol | Amazon Athena |
| **GET** | */distress-list* | Retrieves the list of companies flagged with high distress risk (distress = 1)| Amazon Athena |

#### 5.4.3. Step-by-Step Implementation Guide

- **Step 1: Initialize Amazon Cognito User Pool**
    1. Navigate to Amazon Cognito Console ➔ Click Create user pool.
    2. User pool name: `vietnam-financial-user-pool`.
    3. Configure sign-in options: Email and Username.
    4. Set password complexity standards and configure JWT Token issuance (Access Token & ID Token).
    5. Create a new App Client: `vietnam-financial-web-client`.
    6. Save the `User Pool ID` and `App Client ID`.

- **Step 2: Write AWS Lambda Backend API Source Code (Athena Integration)**
The AWS Lambda source code receives REST API requests from API Gateway, initiates SQL queries on Amazon Athena, and returns formatted JSON data to the Client:


```PYTHON
import json
import boto3
import time

athena_client = boto3.client('athena')
DATABASE = 'vietnam_financial_db'
S3_OUTPUT = 's3://s3-vietnam-financial-curated-data-prod/athena_query_results/'

def lambda_handler(event, context):
    # Lấy tham số mã chứng khoán từ Query String (ví dụ: /api/financial?symbol=VNM)
    params = event.get('queryStringParameters') or {}
    symbol = params.get('symbol', 'VNM')
    
    query = f"""
        SELECT symbol, year, z_score, distress_zone, roa, roe, dar, cr 
        FROM {DATABASE}.financial_features 
        WHERE symbol = '{symbol}' 
        ORDER BY year DESC;
    """
    
    # Thực thi Athena SQL Query
    response = athena_client.start_query_execution(
        QueryString=query,
        QueryExecutionContext={'Database': DATABASE},
        ResultConfiguration={'OutputLocation': S3_OUTPUT}
    )
    
    query_execution_id = response['QueryExecutionId']
    
    # Chờ kết quả truy vấn Athena
    time.sleep(2)
    
    results = athena_client.get_query_results(QueryExecutionId=query_execution_id)
    
    rows = results['ResultSet']['Rows']
    data = []
    headers = [col['VarCharValue'] for col in rows[0]['Data']]
    
    for row in rows[1:]:
        values = [field.get('VarCharValue', '') for field in row['Data']]
        data.append(dict(zip(headers, values)))
        
    return {
        'statusCode': 200,
        'headers': {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*'
        },
        'body': json.dumps({'symbol': symbol, 'financial_data': data}, ensure_ascii=False)
    }
```
- **Step 3: Configure Amazon API Gateway & AWS WAF**
    1. Go to Amazon API Gateway Console ➔ Create new REST API: `vietnam-financial-api`.
    2. Create Resource `/api/financial` and create Method `GET`.
    3. Create Cognito Authorizer: Attach `vietnam-financial-user-pool` as Authorizer to validate JWT Tokens on every request.
    4. Attach AWS WAF (Web Application Firewall) to protect against common web attacks (DDoS, SQL Injection, Cross-Site Scripting).
    5. Click Deploy API to Stage `prod`. Save the `Invoke URL`.