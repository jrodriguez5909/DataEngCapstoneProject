# Udacity Data Engineering Nanodegree | Capstone Project

## Description

The goal of this initiative is to provide answers to questions regarding immigration in the United States. This includes: 

* Identifying the most popular cities for immigration
* Analyzing the gender and visa type distribution of immigrants
* Determining the average age and temperature per month per city. 

I gather information from a variety of sources, including:

* I94 immigration dataset from 2016
* City temperature data from Kaggle
* Demographic information from OpenSoft

My approach involves creating 7 dimension tables and 1 fact table for immigration. I utilize Spark for data extraction, transformation, and loading tasks, and store the final results in the Parquet format for further analysis.

---

## Data Model & Dictionary
![DataModel!](./img/DataModel-Data-Eng-Capstone-Project.png "Data Model")

![DataDictionary!](./img/DataDictionary.png "Data Dictionary")

---

## ETL

The pipeline collects source data from 3 locations, processes it, and saves it as parquet files locally. Afterwards, the processed data is uploaded to Amazon S3. The pattern for processing each table is as follows:

1. Reading raw data
2. Transforming the data
3. Verifying the accuracy of the processed data
4. Saving the processed data in the output folder in parquet format

The project utilizes several tools, including:
- Apache Spark for processing large data sets
- Pandas for easily reading HTML tables
- Amazon S3 for scalable, reliable, fast, and cost-effective storage

Running the pipeline requires 2 further simple steps:
1. Configure the dl.cfg file, using an IAM User with only AmazonS3FullAccess policy for the KEY and SECRET fields and the S3 bucket name for the S3 field.
2. Head to the project's root directory and run the command `python -m etl`.

---

## Further Considerations

**1. Scaling the data** \
If the data volume was increased 100x and Spark is in standalone server mode we should consider using AWS EMR for distributed data processing on the cloud.

**2. A daily 7:00 AM SLA for a dashboard relying on this data** \
Apache Airflow could be used to build an ETL pipeline to regularly update the data and populate the dashboard. Apache Airflow is Python native and integrates well with AWS allowing for quick and easy orchestration.

**3. Database accessibility to over 100 people** \
AWS Redshift can handle up to 500 connections, making it a suitable solution for this requirement. However, a cost/benefit analysis should be conducted before implementing this cloud-based solution.

**4. Mismatch in timeframe across datasets** \
The immigration dataset is from 2016 while the last year in the temperature dataset is 2013 meaning the latter can't be used to observe temperature changes in 2016.

**5. Missing state & city data** \
The label description file is missing state and city information making it difficult to join immigration and demographic tables.