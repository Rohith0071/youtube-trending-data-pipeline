# YouTube Trending Data Pipeline (AWS Serverless Data Engineering Project)

## Project Overview

This project builds a serverless data engineering pipeline on AWS to process and analyze the YouTube Trending Videos dataset.
The pipeline ingests raw data from Kaggle, processes it using AWS Lambda and Python, stores optimized datasets in Amazon S3, catalogs metadata using AWS Glue, enables SQL queries with Amazon Athena, and visualizes insights through Amazon QuickSight dashboards.

The architecture follows a data lake design and uses fully managed AWS services to create a scalable and cost-efficient analytics pipeline.

---

## Dataset

The dataset was downloaded from Kaggle and includes:

* CSV files containing trending video data for multiple regions
* JSON files containing category metadata

These files were initially extracted locally and then uploaded to Amazon S3.

---

## Architecture

The project uses a serverless data pipeline built on AWS.

Data Flow:

Kaggle Dataset → Amazon S3 (Raw Layer) → AWS Lambda (ETL Processing) → Amazon S3 (Analytics Layer in Parquet Format) → AWS Glue Data Catalog → AWS Athena → Amazon QuickSight Dashboards

See the architecture diagram in the **architecture/** folder.

---

## Data Lake Structure

The Amazon S3 bucket is organized into layers to manage data efficiently:

Raw Layer (Landing Zone)
Stores the original CSV and JSON files exactly as downloaded from Kaggle.

Analytics Layer
Stores cleaned and transformed data in Parquet format optimized for analytics queries.

---

## ETL Pipeline (AWS Lambda)

A serverless ETL pipeline was implemented using AWS Lambda.

The Lambda function performs the following steps:

1. Reads CSV and JSON files directly from Amazon S3
2. Uses AWS SDK for Pandas (awswrangler) and pandas for processing
3. Removes duplicate records
4. Handles missing values
5. Converts timestamp fields into proper datetime formats
6. Joins video data with category metadata using the `category_id` field
7. Writes the processed dataset back to S3 in Parquet format

This transformation step improves query performance and reduces storage costs.

---

## Data Catalog (AWS Glue)

AWS Glue Data Catalog is used to store metadata for the processed datasets.

A Glue crawler scans the analytics layer in S3 and automatically:

* Infers the schema
* Creates tables in the Glue database
* Makes the data available for querying through AWS services

---

## Querying Data (Amazon Athena)

Amazon Athena enables SQL-based analysis directly on the data stored in S3.

Example analyses performed:

* Identifying the most viewed videos
* Analyzing engagement metrics (likes and comments)
* Exploring trending categories across different regions

Athena allows querying large datasets without moving them into a separate data warehouse.

---

## Data Visualization (Amazon QuickSight)

Amazon QuickSight is used to build interactive dashboards connected to Athena.

Dashboards include visualizations such as:

* Trending video categories
* Regional engagement patterns
* Top-performing videos by views and likes

These dashboards allow users to explore the dataset through visual analytics.

---

## Technologies Used

* AWS S3 (Data Lake Storage)
* AWS Lambda (Serverless ETL)
* AWS SDK for Pandas (awswrangler)
* Pandas
* AWS Glue Data Catalog
* AWS Athena
* Amazon QuickSight
* Python

---

## Repository Structure

youtube-trending-data-pipeline
│
├── README.md
├── architecture
│   └── architecture.jpeg
├── scripts
│   ├── lambda_function.py
│   └── pyspark_code.py
├── commands
│   └── s3_cli_command.sh

---

## Key Features

* End-to-end serverless data pipeline
* Scalable cloud-based data lake architecture
* Optimized analytics storage using Parquet
* Automated schema discovery using AWS Glue
* SQL-based analysis with Amazon Athena
* Interactive dashboards using Amazon QuickSight

---

## Future Improvements

* Add real-time data ingestion using streaming services
* Implement workflow orchestration with Apache Airflow
* Expand dashboards with additional analytics insights
