# Week 1 Docker-Terraform Homework

## Cohort 2022
### Question 3. Count Records

Answer:

```
SELECT
	COUNT(*) AS trips_count
FROM
	PUBLIC.YELLOW_TAXI_TRIPS
WHERE
	EXTRACT( DAY FROM TPEP_PICKUP_DATETIME) = 15;
```
 Number of taxi trips in January 15: **53024**
 
### Question 4. Largest tip for each day

Answer:

```
SELECT 
	EXTRACT(DAY FROM tpep_pickup_datetime) AS DAY
	, MAX(tip_amount) AS largest_tip 
FROM 
	public.yellow_taxi_trips
WHERE 
	EXTRACT(MONTH FROM tpep_pickup_datetime) = 1
GROUP BY 
	EXTRACT(DAY FROM tpep_pickup_datetime) 
ORDER BY
	largest_tip DESC;
```

 The day with largest tip in january: **20-1-2021** (1140.44$)

 ### Question 5. Most popular destination

Answer:
```
SELECT
	COALESCE(ZDO."Zone", 'Unknown') AS DESTINATION,
	COUNT(*) AS TRIP_COUNT
FROM
	PUBLIC.YELLOW_TAXI_TRIPS Y
	JOIN PUBLIC.ZONES ZPU ON Y."PULocationID" = ZPU."LocationID"
	JOIN PUBLIC.ZONES ZDO ON Y."DOLocationID" = ZDO."LocationID"
WHERE
	ZPU."Zone" = 'Central Park'
	AND EXTRACT( MONTH FROM Y.TPEP_PICKUP_DATETIME) = 1
	AND EXTRACT( DAY FROM Y.TPEP_PICKUP_DATETIME) = 14
GROUP BY
	ZDO."Zone"
ORDER BY
	TRIP_COUNT DESC
LIMIT
	1;
```
Most popular destination: **Upper East Side South** with 97 trips from central park on January 14


### Question 6. Most expensive locations

Answer:
```
SELECT
	CONCAT(
		COALESCE(ZPU."Zone", 'Unknown'),
		' / ',
		COALESCE(ZDO."Zone", 'Unknown')
	) AS PICKUP_DROPOFF_PAIR,
	AVG(Y.TOTAL_AMOUNT) AS AVG_TOTAL_AMOUNT
FROM
	PUBLIC.YELLOW_TAXI_TRIPS Y
	JOIN PUBLIC.ZONES ZPU ON Y."PULocationID" = ZPU."LocationID"
	JOIN PUBLIC.ZONES ZDO ON Y."DOLocationID" = ZDO."LocationID"
GROUP BY
	CONCAT(
		COALESCE(ZPU."Zone", 'Unknown'),
		' / ',
		COALESCE(ZDO."Zone", 'Unknown')
	)
ORDER BY
	AVG(Y.TOTAL_AMOUNT) DESC
```
The pickup-dropoff pair with the largest average price: Alphabet City / Outside of NYC (2292.4$)


## Cohort 2023
### Question 1. Knowing docker tags

Answer:
` docker build --help `

Correct choice is: ` --iidfile string `

### Question 2. Understanding docker first run

Answer: 
` docker run -it --entrypoint bash python:3.9 `

`pip list`

Output: 
```
Package    Version
---------- -------
pip        23.0.1
setuptools 58.1.0
wheel      0.45.1
```
Correct choice is: 3

### Question 3. Count Records

Answer: 
```
SELECT
	COUNT(*) AS TRIPS_COUNT
FROM
	PUBLIC.GREEN_TAXI_TRIPS
WHERE
	LPEP_PICKUP_DATETIME::DATE = '2019-01-15'
	AND LPEP_DROPOFF_DATETIME::DATE = '2019-01-15';
```
Correct choice is: 20530

### Question 4. Largest trip for each day

Answer:
```

	SELECT
	LPEP_PICKUP_DATETIME::DATE AS DATE,
	MAX(TRIP_DISTANCE) AS LARGEST_TRIP
FROM
	PUBLIC.GREEN_TAXI_TRIPS
GROUP BY
	LPEP_PICKUP_DATETIME::DATE
ORDER BY
	LARGEST_TRIP DESC
LIMIT
	1;
```
Correct choice is: 2019-01-15

### Question 5. The number of passengers

Answer:
```
SELECT
	PASSENGER_COUNT,
	COUNT(*) AS TRIP_COUNT
FROM
	PUBLIC.GREEN_TAXI_TRIPS
WHERE
	LPEP_PICKUP_DATETIME::DATE = '2019-01-01'
	AND PASSENGER_COUNT IN (2, 3)
GROUP BY
	PASSENGER_COUNT;
```
Correct choice is: 2: 1282 ; 3: 254

### Question 6. Largest tip

Answer:
```
SELECT
	ZDO."Zone",
	G.TIP_AMOUNT
FROM
	PUBLIC.GREEN_TAXI_TRIPS G
	JOIN PUBLIC.ZONES ZPU ON ZPU."LocationID" = G."PULocationID"
	JOIN PUBLIC.ZONES ZDO ON ZDO."LocationID" = G."DOLocationID"
WHERE
	ZPU."Zone" = 'Astoria'
ORDER BY
	TIP_AMOUNT DESC;
```
Correct choice is: Long Island City/Queens Plaza


## Cohort 2024

### Question 1. Knowing docker tags

Answer: 

`docker run --help`

Correct choice is: `--rm`


### Question 2. Understanding docker first run

Answer: 
` docker run -it --entrypoint bash python:3.9 `

`pip list`

Output: 
```
Package    Version
---------- -------
pip        23.0.1
setuptools 58.1.0
wheel      0.45.1
```
Correct choice is: 0.45.1

### Question 3. Count records

Answer:
```
SELECT
	COUNT(*) AS TRIPS_COUNT
FROM
	PUBLIC.GREEN_TAXI_TRIPS_09
WHERE
	LPEP_PICKUP_DATETIME::DATE = '2019-09-18'
	AND LPEP_DROPOFF_DATETIME::DATE = '2019-09-18';
```
Correct choice is: 15612

### Question 4. Longest trip for each day

Answer:
```
SELECT
	COUNT(*) AS TRIPS_COUNT
FROM
	PUBLIC.GREEN_TAXI_TRIPS_09
WHERE
	LPEP_PICKUP_DATETIME::DATE = '2019-09-18'
	AND LPEP_DROPOFF_DATETIME::DATE = '2019-09-18';

SELECT
	LPEP_PICKUP_DATETIME::DATE,
	MAX(TRIP_DISTANCE) AS LONGEST_TRIP
FROM
	PUBLIC.GREEN_TAXI_TRIPS_09
GROUP BY
	LPEP_PICKUP_DATETIME::DATE
ORDER BY
	LONGEST_TRIP DESC LIMIT
	1;
```
Correct choice is: 2019-09-26

### Question 5. Three biggest pick up Boroughs

Answer:
```
SELECT
	ZPU."Borough",
	SUM(TOTAL_AMOUNT) AS SUM_TOTAL
FROM
	PUBLIC.GREEN_TAXI_TRIPS G
	JOIN PUBLIC.ZONES ZPU ON ZPU."LocationID" = G."PULocationID"
	JOIN PUBLIC.ZONES ZDO ON ZDO."LocationID" = G."DOLocationID"
WHERE
	ZPU."Borough" != 'Unknown'
GROUP BY
	ZPU."Borough"
HAVING
	SUM(TOTAL_AMOUNT) > 50000
ORDER BY
	SUM_TOTAL DESC
LIMIT
	3;
```
Correct choice is: "Brooklyn" "Manhattan" "Queens"


### Question 6. Largest tip
Answer:
```
SELECT
	ZDO."Zone" as dropoff_zone,
	max(Tip_AMOUNT) AS largest_tip
FROM
	PUBLIC.GREEN_TAXI_TRIPS G
	JOIN PUBLIC.ZONES ZPU ON ZPU."LocationID" = G."PULocationID"
	JOIN PUBLIC.ZONES ZDO ON ZDO."LocationID" = G."DOLocationID"
WHERE
	ZPU."Zone" = 'Astoria'
GROUP BY
	ZDO."Zone"
ORDER BY
	largest_tip DESC
LIMIT 1;
```
The correct choice is: Long Island City/Queens Plaza
