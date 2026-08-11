---
title: "Week 4 - Financial Data Ingestion Pipeline Design and Implementation"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---



### Week 4 Overview

During Week 4, I focused on designing and implementing the core data ingestion pipeline for the **Financial Data Lake** project. The week began with evaluating different cloud architectures and selecting an appropriate serverless design. Based on the selected architecture, I implemented the initial ingestion workflow, including provider validation, adapter development, batch processing, and scalability evaluation for collecting Vietnamese stock market data.

| Domain | Main Focus | Key Takeaway |
| --- | --- | --- |
| A | Architecture Evaluation & Pipeline Design | Comparing different cloud architectures helps identify a scalable, cost-efficient, and maintainable solution for financial data ingestion.
| B | Data Ingestion Pipeline Implementation | Building reusable provider adapters and ingestion workers establishes a reliable foundation for automated data collection.
| C | Batch Processing & Scalability Validation | Implementing retry, checkpoint, and batch execution mechanisms improves pipeline robustness and prepares the system for larger-scale data ingestion.
---
### Domain A: ARCHITECTURE EVALUATION & PIPELINE DESIGN

#### *Mon, Jul 13 | Evaluating Financial Data Lake Architectures*

- Studied different architectural approaches for building a **Financial Data Lake**, including traditional container-based deployment and serverless event-driven architecture.
- Compared deployment complexity, scalability, operational cost, and maintainability between **RDS-based** and **Amazon S3-based** solutions.
- Reviewed the proposed AWS Serverless Financial Data Lake architecture, including:
  - Amazon EventBridge
  - AWS Lambda
  - Amazon SQS
  - Amazon S3
  - AWS Glue Catalog
  - Amazon Athena
  - Amazon API Gateway
- Analyzed how each service contributes to data ingestion, processing, storage, and analytics.
- Ref: Architecture Comparison Document

> Key takeaway: A serverless architecture significantly reduces operational complexity while providing automatic scalability and cost-efficient processing for periodic financial data collection.

#### *Tue, Jul 14 | Designing the Local Data Ingestion Pipeline*

- Designed the overall ingestion workflow before cloud deployment.
Defined the responsibilities of Universe Loader, Provider Adapter, Dispatcher, Worker, and Validator components.
- Finalized the initial universe of listed companies and validated data availability using provider smoke tests.
- Planned the local Bronze storage structure for storing raw JSON responses before ETL processing.
- Ref: Implementation Guide Draft

> Key takeaway: Separating provider abstraction, ingestion workers, and validation logic improves modularity and simplifies future migration from local execution to AWS services.
---
### Domain B: DATA INGESTION PIPELINE IMPLEMENTATION

#### *Wed, Jul 15 | Developing Provider Adapter & Ingestion Worker*

- Implemented the **Provider Adapter** responsible for retrieving OHLCV data from the selected financial data source.
- Developed **Ingestion Workers** capable of processing multiple stock tickers sequentially.
- Added **Retry** and **Backoff** mechanisms to improve reliability during temporary provider failures.
- Implemented structured logging for ticker symbols, execution time, provider status, and ingestion results.
- Ref: Implementation Guide Draft

> Key takeaway: Retry strategies and centralized logging greatly improve pipeline stability without increasing implementation complexity.

#### *Thu, Jul 16 | Local Batch Execution & Pipeline Validation*

- Executed batch ingestion using the selected universe of stock tickers.
- Validated raw data completeness and classified successful and failed requests.
- Tested **checkpoint handling** to ensure interrupted executions could resume without restarting the entire batch.
- Evaluated local storage organization for** Raw JSON** outputs and prepared the pipeline for future **Curated** processing.
- Ref: *Implementation Guide Draft*

> Key takeaway: Batch execution combined with checkpoint recovery improves fault tolerance and minimizes unnecessary reprocessing.
---
### Domain C: Batch Processing & Scalability Validation

#### *Fri, Jul 17 | Scalability Evaluation & Future Pipeline Planning*

- Evaluated pipeline scalability when increasing the number of processed stock tickers.
- Reviewed concurrency strategies, conservative rate limiting, and provider request scheduling.
- Studied how the ingestion pipeline can be integrated with future ETL, Feature Store, and Predictive Analytics components.
- Identified future enhancements for machine learning integration using curated financial datasets.
- Ref: Predictive Analytics Proposal

> Key takeaway: Designing the ingestion pipeline with scalability and modularity in mind enables seamless integration with downstream analytics and machine learning workflows.
---
### Achievements

- Evaluated and selected an appropriate serverless architecture for the **Financial Data Lake** project.
- Designed the overall local data ingestion workflow and finalized the initial stock universe.
- Implemented reusable **provider adapters** with **retry**, **logging**, and **validation** mechanisms.
- Established the foundation for scalable batch ingestion using **checkpoint** and **fault recovery** strategies.
- Prepared the ingestion pipeline for future ETL processing, feature engineering, and **predictive analytics** integration.