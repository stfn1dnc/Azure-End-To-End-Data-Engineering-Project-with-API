# Azure-End-To-End-Data-Engineering-Project-with-API

Project Overview
This project implements a comprehensive Data Engineering solution for extracting, processing, and analyzing global seismic data provided by the USGS (U.S. Geological Survey) API. The workflow is fully automated within the Microsoft Azure ecosystem, following industry best practices for cloud data architecture.

Architecture & Technologies
The solution follows a Medallion (Bronze-Silver-Gold) architecture to ensure data quality and reliability as it moves through the pipeline:

Orchestration: Azure Data Factory (Workflow control and dynamic date parameterization).

Compute: Azure Databricks (Distributed processing using PySpark).

Storage: Azure Data Lake Storage (ADLS) Gen2 (Layered data storage).

Data Warehouse: Azure Synapse Analytics (Serverless SQL Pool for final analytical serving).

Languages: Python (PySpark), SQL.

Data Formats: JSON (Raw), Parquet (Optimized).


Pipeline Flow (ETL)
1. Ingestion (Bronze Layer)
Data is extracted from the USGS REST API via a Databricks Ingestion notebook triggered by ADF. The pipeline uses dynamic parameters (start_date and end_date) to allow for incremental daily runs. Data is persisted in its raw JSON format.

2. Transformation (Silver Layer)
In this stage, data is cleaned and structured:

Data Type Casting: Converting timestamps and numeric values.

Data Quality: Handling null values and filtering invalid geographic coordinates.

Schema Enforcement: Ensuring consistency across the dataset.

3. Aggregation (Gold Layer)
The final processing layer prepares data for analytics:

Risk Classification: Implementing logic to categorize events into risk classes (Low, Moderate, High) based on significance scores.

Storage Optimization: Saving the final dataset in Parquet format, partitioned for high-performance reading.

4. Serving (Synapse Load)
An ADF Copy Data activity automatically moves the Gold Parquet files into a dedicated SQL table in Azure Synapse Analytics using the Auto-create table functionality.

Setup & Usage
Notebooks: Import the scripts from the /notebooks directory into your Databricks workspace.

Connections: Set up Linked Services in Azure Data Factory for Databricks and Synapse.

Execution: Trigger the pipeline by providing the desired date range in the ADF Trigger/Debug parameters.

👤 Author
Stefan Danci Master's Student: Business Analytics and Management of Information (BAMI) - FSEGA Technical Professional based in Cluj-Napoca
