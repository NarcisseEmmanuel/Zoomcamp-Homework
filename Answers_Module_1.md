## Answers to questions from Module 1

### 1. Understanding docker images
Code to launch Docker with the Python 3.13 image. Use a bash entry point to interact with the container and the code for the pip version.

```bash
docker run -it --rm --entrypoint=bash python:3.13 /
pip --version /
```

### 3. For the trips in November 2025, how many trips had a trip_distance of less than or equal to 1 mile

```bash
 SELECT COUNT(*) AS nb_trips
 FROM green_taxi_data
 WHERE lpep_pickup_datetime >= '2025-11-01'
   AND lpep_pickup_datetime < '2025-12-01'
   AND trip_distance <= 1;
```

### 4.Which was the pick up day with the longest trip distance? Only consider trips with trip_distance less than 100 miles

````bash
SELECT DATE(lpep_pickup_datetime) AS pickup_day,
       MAX(trip_distance) AS max_trip_distance
FROM green_taxi_data
WHERE trip_distance < 100
GROUP BY DATE(lpep_pickup_datetime)
ORDER BY max_trip_distance DESC
LIMIT 1;
````

### 5.Which was the pickup zone with the largest total_amount (sum of all trips) on November 18th, 2025

````bash
SELECT
    z."Zone" AS pickup_zone,
    SUM(t.total_amount) AS total_revenue
FROM green_taxi_data t
JOIN taxi_zone z
    ON t."PULocationID" = z."LocationID"
WHERE t.lpep_pickup_datetime >= '2025-11-18'
  AND t.lpep_pickup_datetime < '2025-11-19'
GROUP BY z."Zone"
ORDER BY total_revenue DESC
LIMIT 1;

````

### 6. For the passengers picked up in the zone named "East Harlem North" in November 2025, which was the drop off zone that had the largest tip

`````bash
SELECT t."DOLocationID", z."Zone", MAX(t.tip_amount) AS max_tip
FROM green_taxi_data t
JOIN taxi_zone z on z."LocationID" = t."DOLocationID"
WHERE t."PULocationID" = 74
GROUP BY t."DOLocationID", z."Zone"
ORDER BY max_tip desc;
````
