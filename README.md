# 🚀 Azure Data Engineering Pipeline – Metadata-Driven Ingestion

## 📌 Overview

This project implements a scalable, metadata-driven data ingestion pipeline using Azure services. It dynamically ingests multiple tables from Azure SQL Database into ADLS Gen2 using incremental logic, parallel processing, and robust error handling.

## 🏗️ Architecture
Azure SQL DB → ADF → ADLS Gen2 (Bronze Layer) → Databricks (Planned)

## ⚙️ Tech Stack

- Azure Data Factory
- Azure SQL Database
- Azure Data Lake Storage Gen2
- Azure Databricks (planned for transformation layer)

## 🔷 Key Features

- Metadata-driven ingestion (control table)
- Incremental load using watermark
- Parallel processing using ForEach (batch control)
- Conditional execution (skip if no new data)
- Error handling with logging framework
- Dynamic pipeline for multiple tables
- Partitioned storage in ADLS

## 🔷 Pipeline Design

### 🔹 Master Pipeline

- Reads active tables from control table
- Executes ingestion using ForEach (parallel processing)

### 🔹 Ingestion Logic

- Log Start
- Check for new data (watermark)
- If data exists:
  - Copy to ADLS
  - Get MAX watermark
  - Update watermark
  - Log Success
- Else:
  - Log NO_DATA
- On failure:
  - Log error

## 🔷 ADLS Storage Pattern

/bronze/
/table_name/
/year=YYYY/month=MM/day=DD/

## 🔷 Error Handling

- Retry logic for Copy activity
- Failure path logging
- Status tracking (SUCCESS / FAILED / NO_DATA)

## 🔷 Watermark Strategy

- Incremental load using watermark column
- Safe update using stored procedure
- Designed to avoid data loss

## 🔷 Next Enhancements

- Databricks integration for Silver & Gold layers
- Delta Lake implementation
- CDC-based ingestion
- Data validation framework

## 🔷 Author

**Susmita Biswas**  
Azure Data Engineer | Databricks Certified
