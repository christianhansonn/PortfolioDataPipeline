# Data Pipeline: Transforming and Loading Customer Data

## Introduction

This project is to showcase skills in cloud computing, ETL, data pipeline and visualization creation. 

I utilize the following technologies and languages:


1. S3 to store the data 
2. AWS Athena and SQL to query the data before ETL 
3. Python to write custom transformation logic 
4. AWS Glue to execute the ETL process 
5. AWS RDS to store the transformed data 
6. AWS Quicksight to visualize the transformed data 

![Data Pipeline Flow Chart](https://github.com/christianhansonn/PortfolioDataPipeline/blob/main/static/Portfolio%20Project%20Pipeline.jpeg)

# Deploying in AWS

## AWS Glue ETL and RDS

- I wrote this [Python script](https://github.com/christianhansonn/PortfolioDataPipeline/blob/main/Glue/clean.ipynb) to utilize in my AWS Glue Crawler
- Preformed the extract and transform process to manipulate the dataset in S3
- Loaded the cleaned data into Aurora Serverless MySQL database


## Querying and Visualizing the Cleaned Data

Utilizing the following SQL script to query the Aurora database, I now have a list of paying customer and their contact information

```sql

SELECT
    CONCAT(first_name,' ',last_name) AS Name ,
    phone_number ,
    street_address ,
    state ,
    zip
FROM
    ch_de_portfolio_project_cleaned_customer
WHERE
    paying_customer != 'Y'
ORDER BY 1

```

This query can later be utilized in Quicksight to distribute to call center teams and create KPIs for leadership
