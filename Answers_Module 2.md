
## Answers to questions from Module 2


### 3. How many rows are there for the Yellow Taxi data for all CSV files in the year 2020?
```bash
 SELECT count(*) 
FROM zoomcamp.yellow_tripdata
WHERE filename LIKE 'yellow_tripdata_2020-%.csv'
```

### 4. How many rows are there for the `Green` Taxi data for all CSV files in the year 2020?

````bash
SELECT count(*) 
FROM zoomcamp.green_tripdata
WHERE filename LIKE 'green_tripdata_2020-%.csv';
````

### 5.  How many rows are there for the `Yellow` Taxi data for the March 2021 CSV file?

````bash
SELECT count(*) 
FROM zoomcamp.yellow_tripdata
WHERE filename LIKE 'yellow_tripdata_2021-03.csv';
````

### 6. How would you configure the timezone to New York in a Schedule trigger?

`````bash
triggers:
  - id: yellow_schedule
    type: io.kestra.plugin.core.trigger.Schedule
    cron: "0 10 1 * *"
    timezone: "America/New_York" # <--- Ici
    inputs:
      taxi: yellow
````
