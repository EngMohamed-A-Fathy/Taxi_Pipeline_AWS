
# Taxi Case Study Project - AWS Data Pipeline
## Overview
The Taxi Case Study project revolves around taxis in New York City and involves the implementation of a data pipeline using various AWS services. This project was developed as part of the Data Management track at ITI. The decision to utilize AWS for our pipeline was driven by the numerous advantages offered by the AWS Cloud, including scalability, reliability, and security.

## AWS Services Used
The pipeline makes use of the following AWS services:

### Amazon S3 (Simple Storage Service): 
Serves as a highly scalable object storage service and acts as the initial destination for the source files.

### AWS Lambda: 
A serverless compute service used to process data. It reads the source files, randomly selects a number of records, and saves them to Amazon DynamoDB. It also handles the extraction and storage of selected records back to S3.

### Amazon DynamoDB: 
A NoSQL database service utilized as a checkpoint to prevent duplicate data transmission and as a staging area for real-time streaming.

### Amazon Kinesis:
Acts as a data ingestion layer for real-time streaming, capturing data from the Lambda producer and feeding it to the consumer process.

### Amazon Athena:
An interactive query service used to fetch real-time streaming data from DynamoDB for creating real-time dashboards.

#### Power BI:
A business analytics tool used to visualize real-time data fetched from Athena and create real-time monitoring dashboards.

### Amazon Redshift:
A powerful data warehousing solution used to store historical data extracted at the end of each day.

### Amazon QuickSight:
A cloud-based business intelligence tool used to create analytical dashboards, providing insights into historical patterns and trends.

## Data Pipeline Flow
The data pipeline consists of the following steps:

1- Source files are uploaded to Amazon S3, serving as the starting point of the pipeline.

2- AWS Lambda processes the source files, randomly selects a number of records, and saves them to DynamoDB.

3- The selected records are subtracted from the DynamoDB table and saved back to S3.

4- A Lambda producer is triggered when new data is available in S3. It sends the data to an Amazon Kinesis stream for real-time streaming.

5- A consumer process retrieves the real-time streaming data from Kinesis and stores it in DynamoDB.

6- For real-time streaming, Amazon Athena fetches data from DynamoDB to create real-time monitoring dashboards.

7- Real-time data is backed up on S3, and Power BI automatically refreshes every 30 seconds to visualize the real-time dashboard.

8- For analytical dashboard generation, a Lambda function extracts data specific to each day and stores it in S3.

9- Another Lambda function retrieves this historical data from S3 and writes it into an Amazon Redshift table.

10- Amazon QuickSight copies the data from Redshift and creates an analytical dashboard, providing insights into historical patterns and trends.
## Conclusion
By combining the capabilities of various AWS services, the Taxi Case Study project delivers a robust and scalable data pipeline for processing taxi-related data in real-time and generating analytical insights for informed decision-making. The use of AWS services ensures efficiency, reliability, and security throughout the data pipeline. This case study project showcases the potential of AWS cloud services for managing and analyzing large volumes of data effectively.
