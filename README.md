# Data Pipeline: Transforming and Loading Customer Data

## Introduction

This project is to showcase skills in cloud computing, ETL, data pipeline and visualization creation. 

I utilize the following technologies and languages:

<ul> 
<li> S3 to store the data </li>
<li> AWS Athena and SQL to query the data before ETL </li>
<li> Python to write custom transformation logic </li>
<li> AWS Glue to execute the ETL process </li>
<li> AWS RDS to store the transformed data </li>
<li> AWS Quicksight to visualize the transformed data </li>
</ul>


## Prerequisite

<ul>
    <li> Download [dataset](https://github.com/christianhansonn/PortfolioDataPipeline/blob/main/S3/customer_call_list.csv) from Kaggle </li>
    <li> Create S3 bucket for storage </li>
    <li> Create Aurora Servless DB and customer table with [SQL command](https://github.com/christianhansonn/PortfolioDataPipeline/blob/main/RDS/create_table.sql) </li>
</ul>

![Data Pipeline Flow Chart](https://github.com/christianhansonn/PortfolioDataPipeline/blob/main/static/Portfolio%20Project%20Pipeline.jpeg)

# Deploying in AWS

## Query Structured Data Before ETL

Using AWS Athena and SQL, I query the stored CSV file to identify transformations that will need to be done

```

SELECT *
FROM customer_call_list.csv

```


## AWS Glue ETL and RDS

I wrote this [Python script](https://github.com/christianhansonn/PortfolioDataPipeline/blob/main/Glue/clean.ipynb) to utilize in my AWS Glue Crawler, preformed the ETL process, and loaded the cleaned data into Aurora Serverless MySQL database

## Querying and Visualizing the Cleaned Data

Utilizing the following SQL script to query the Aurora database, I now have a list of paying customer and their contact information

```

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
