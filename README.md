# **Flight Booking Analytics Data Pipeline using Airflow and Github Actions**
***
## Project Overview
Designed and implemented a serverless data engineering pipeline on Google Cloud Platform (GCP) to process and analyze flight booking data.
The solution leverages Apache Airflow (Cloud Composer) for orchestration, Dataproc Serverless (Spark) for distributed data processing, and BigQuery for analytics-ready data storage. CI/CD automation is implemented using GitHub Actions to ensure consistent and reliable deployments.
***
## Architectural Diagram
![Architecture Design](https://github.com/srirangam-saitej/Flights_Booking_Pipeline/blob/54c7bf66884b8a0120d33297c18540b7bbdbbfa6/images/Flight_Booking_Pipeline_Flow.png)
***
## Key Steps
### 1.Create a Composer Enviroment for the Pipeline
![Composer](https://github.com/srirangam-saitej/Flights_Booking_Pipeline/blob/54c7bf66884b8a0120d33297c18540b7bbdbbfa6/images/dags_github_action.png)
### 2.Create a Bigquery Dataset which is required for creating the tables
![Bigquery](https://github.com/srirangam-saitej/Flights_Booking_Pipeline/blob/baab8a9f737bd20e6e94a32914562291951209d4/images/bigquery_dataset.png)
### 3.Create a Bucket in GCP which will be used for placing the source files and spark code
![Bucket](https://github.com/srirangam-saitej/Flights_Booking_Pipeline/blob/f446234f1e443b46cccc1b7ce26c87a3ef7a3451/images/bucket_flight.png)
### 4.We use a Github actions for CI/CD in this pipeline Design
- Once a commit is done to Github repo,tasks that are automated through Github Actions
  ![Github](https://github.com/srirangam-saitej/Flights_Booking_Pipeline/blob/f446234f1e443b46cccc1b7ce26c87a3ef7a3451/images/Github_action_Dev.png)
   -  copy the variables.json file from repo to /DAG-bucket/data/dev/variables.json
   -  copy the variables.json from the above DAG folder to DAG UI,which can be checked in Admin--->variables
   ![variables](https://github.com/srirangam-saitej/Flights_Booking_Pipeline/blob/f446234f1e443b46cccc1b7ce26c87a3ef7a3451/images/DAG%20variables.png)
   -  places the DAG from repo to /DAG-bucket/dags/airflow_job.py
   -  copies the spark file from repo to /flights-booking-pipeline/flights-booking-analysis/spark-job/spark_transformation_job.py
### 5.Place the input file flight_booking.csv in this bucket path flights-booking-pipeline/flights-booking-analysis/source-dev/flight_booking.csv,which triggers the DAG.
![DAG](https://github.com/srirangam-saitej/Flights_Booking_Pipeline/blob/f446234f1e443b46cccc1b7ce26c87a3ef7a3451/images/DAG.png)
### 6.Once the File sensor activity is completed,we can see a Dataproc serverless batch is triggered,where spark processing gets triggered.For every serverless batch trigger a new unique batch id is passed which is handled through the code.
![Dataproc](https://github.com/srirangam-saitej/Flights_Booking_Pipeline/blob/f446234f1e443b46cccc1b7ce26c87a3ef7a3451/images/Dataproc%20serverless%20batches.png)
### 7.Once the dataproc job is sucessful,we can see the transformed data is loaded into BigQuery tables
![BigQuery Tables](https://github.com/srirangam-saitej/Flights_Booking_Pipeline/blob/f446234f1e443b46cccc1b7ce26c87a3ef7a3451/images/Bigquery%20tables.png)
***
## Pipeline Design on Azure
![Azure](https://github.com/srirangam-saitej/Flights_Booking_Pipeline/blob/de32594d32f164f1d776fcb1b0ec720f585f733f/images/azure%20pipeline.png)
