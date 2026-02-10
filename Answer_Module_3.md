
## Answers to questions from Module 3


### 1. What is count of records for the 2024 Yellow Taxi Data??
```bash
 SELECT COUNT(*) FROM kestra-learn.ny_taxi.external_yellow_tripdata_2024;
```

### 2. Write a query to count the distinct number of PULocationIDs for the entire dataset on both the tables.
What is the estimated amount of data that will be read when this query is executed on the External Table and the Table?
````bash
SELECT COUNT(DISTINCT PULocationID)
FROM kestra-learn.ny_taxi.external_yellow_tripdata_2024;

SELECT COUNT(DISTINCT PULocationID)
FROM kestra-learn.ny_taxi.yellow_tripdata_2024_non_partitionne;
````

### 3.  Write a query to retrieve the PULocationID from the table (not the external table) in BigQuery. Now write a query to retrieve the PULocationID and DOLocationID on the same table. Why are the estimated number of Bytes different?

````bash
SELECT PULocationID
FROM kestra-learn.ny_taxi.yellow_tripdata_2024_non_partitionne;

SELECT PULocationID, DOLocationID
FROM kestra-learn.ny_taxi.yellow_tripdata_2024_non_partitionne;
````

### 4. How many records have a fare_amount of 0?
````bash
SELECT COUNT(*)
FROM kestra-learn.ny_taxi.external_yellow_tripdata_2024
WHERE fare_amount = 0;

````

### 6. Write a query to retrieve the distinct VendorIDs between tpep_dropoff_datetime 2024-03-01 and 2024-03-15 (inclusive)

Use the materialized table you created earlier in your from clause and note the estimated bytes. Now change the table in the from clause to the partitioned table you created for question 5 and note the estimated bytes processed. What are these values?
````bash
CREATE OR REPLACE TABLE  kestra-learn.ny_taxi.yellow_tripdata_2024_partitionne
PARTITION BY
  DATE(tpep_dropoff_datetime) AS
SELECT * FROM kestra-learn.ny_taxi.external_yellow_tripdata_2024;

SELECT DISTINCT VendorID
FROM kestra-learn.ny_taxi.yellow_tripdata_2024_partitionne
WHERE tpep_dropoff_datetime >= '2024-03-01' 
  AND tpep_dropoff_datetime <= '2024-03-15';


SELECT DISTINCT VendorID
FROM kestra-learn.ny_taxi.yellow_tripdata_2024_non_partitionne
WHERE tpep_dropoff_datetime >= '2024-03-01' 
  AND tpep_dropoff_datetime <= '2024-03-15';

````
