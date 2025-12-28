# Real-Time Cryptocurrency Data Engineering Pipeline

 
### Project Overview

This project demonstrates a complete **end-to-end data engineering pipeline** for ingesting, processing, and analyzing **real-time cryptocurrency market data** using modern cloud and big data tools.

The pipeline simulates a real-world production setup where **live data** is streamed using **Apache Kafka**, stored in **Amazon S3**, transformed using **AWS Glue with PySpark**, and queried using **Amazon Athena** for analytics.

The goal of this project is to showcase **core data engineering concepts**, hands-on cloud skills, and practical **ETL workflows** that are commonly used in industry.


### Architecture Overview

#### High-level flow:

#### 1. Data Source
* Cryptocurrency market data is fetched from the CoinCap API.

#### 2. Streaming Ingestion (Apache Kafka)
* An Amazon EC2 instance is created to host the Kafka broker.
* The EC2 instance is accessed using SSH from the local machine.
* Apache Kafka is installed and configured on the EC2 instance.
* Kafka services are started manually on the EC2 host.
* A Kafka Producer publishes live cryptocurrency data to Kafka topics.
* A Kafka Consumer subscribes to these topics and reads the streaming data in real time.

#### 3. Raw Storage (Amazon S3 – Raw Zone)
* Kafka consumer writes raw JSON data into Amazon S3
* This represents the raw / landing layer of the data lake

#### 4. ETL Processing (AWS Glue – PySpark)
* AWS Glue reads raw JSON files from S3
* Applies schema enforcement, data cleaning, and transformations
* Converts JSON into Parquet format
* Writes processed data to a curated S3 path

#### 5. Metadata Management (AWS Glue Crawler)
* Crawlers scan curated data
* Create tables in AWS Glue Data Catalog

#### 6. Analytics & Querying (Amazon Athena)
* Athena queries curated Parquet data directly from S3
* Enables fast, serverless SQL analytics

### Technologies Used
* Apache Kafka – Real-time data streaming
* Python – API ingestion and Kafka producers/consumers
* Amazon EC2 – Kafka broker hosting
* Amazon S3 – Data lake storage (raw & curated zones)
* AWS Glue – ETL processing using PySpark
* PySpark – Data transformations and schema handling
* AWS Glue Data Catalog – Metadata management
* Amazon Athena – Serverless SQL querying

### Detailed Pipeline Steps
**1. Kafka Streaming Layer**
* An Amazon EC2 instance is created to host the Kafka broker and it is accessed using ssh through local machines's command prompt.
* A Kafka Producer fetches live crypto data from the CoinCap API and the producer publishes messages to a Kafka topic.
* A Kafka Consumer subscribes to the topic and continuously reads messages.
* Incoming messages are saved as raw JSON files in Amazon S3.
* This simulates a real-time ingestion system commonly used in production pipelines.

**2. Raw Data Storage (S3 – Raw Zone)**
* Raw data is stored exactly as received (JSON format).
* No transformations are applied at this stage.
* This ensures data traceability and allows reprocessing if needed.

**3. ETL Processing with AWS Glue (PySpark)**
An AWS Glue job performs the following:
* Reads raw JSON files from S3
* Applies an explicit schema using PySpark
* Handles type casting and null values
* Flattens nested structures (using explode() where needed)
* Converts JSON data into columnar Parquet format
* Writes cleaned data into the curated S3 path

**Why Parquet?**
* Faster query performance
* Lower storage cost
* Optimized for analytics

**4. Metadata Creation with Glue Crawler**
* Glue Crawlers scan the curated S3 folder
* Automatically infer schema and partitions
* Create tables in AWS Glue Data Catalog
* Makes data discoverable by Athena

**5. Analytics with Amazon Athena**
* Athena queries the curated Parquet data directly from S3
* No database or servers to manage
* SQL queries return analytics-ready results

### Key Data Engineering Concepts Demonstrated
* Real-time streaming with Kafka
* Event-driven ingestion
* Data lake architecture (raw vs curated zones)
* ETL using PySpark
* Schema enforcement and evolution
* JSON to Parquet conversion
* Partition-aware querying
* Serverless analytics with Athena
* Cloud-native data engineering on AWS

🧠 What This Project Shows Interviewers

You understand how real data pipelines are built

You know when to use Kafka vs batch processing

You can write PySpark ETL jobs

You understand S3 + Glue + Athena architecture

You know why Parquet is used

You can explain raw → curated → analytics layers

🚀 Future Improvements (Optional)

Add Kafka Connect for S3 sink

Add data quality checks in Glue

Automate Glue jobs using Airflow

Add dashboards using Amazon QuickSight

Implement partitioning by date/hour

### Conclusion
This project replicates a **real-world data engineering workflow** using industry-standard tools.
It demonstrates how **streaming data** can be ingested, transformed, stored efficiently, and queried at scale in a **cloud-native environment**.
