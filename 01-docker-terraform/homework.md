## Question 1. Knowing docker tags
`docker run --help`

Answer: `rmi`


### Question 2. Understanding docker first run
` docker run -it --entrypoint bash python:3.12.8 `

`pip list`

Answer: ``24.3.1``

## Question 3. Count records
How many taxi trips were made on October 18th, 2019?

(Trips that started and finished on that day)

Answer: <mark>17417</mark>
```sql
SELECT
	COUNT(*)
FROM
	PUBLIC.GREEN_TAXI_DATA
WHERE
	DATE (LPEP_PICKUP_DATETIME) = '2019-10-18'
	AND DATE (LPEP_DROPOFF_DATETIME) = '2019-10-18';
```
## Question 4. Longest trip for each day
Which was the pick up day with the longest trip distance? Use the pick up time for your calculations.

Answer: <mark>2019-10-31</mark>
```sql
SELECT
	EXTRACT( DAY FROM LPEP_PICKUP_DATETIME) AS DAY,
	MAX(TRIP_DISTANCE) AS LONGEST_TRIP_DISTANCE
FROM
	PUBLIC.GREEN_TAXI_DATA
GROUP BY
	1
ORDER BY
	2 DESC
LIMIT
	1;
```
## Question 5. Three biggest pickup zones
Which where the top pickup locations with over 13,000 in total_amount (across all trips) for 2019-10-18?

Consider only lpep_pickup_datetime when filtering by date.

Answer: <mark>East Harlem North, East Harlem South, Morningside Heights</mark>
```sql
SELECT
	PUZ."Zone" AS PICKUP_LOCATION,
	SUM(G.TOTAL_AMOUNT)
FROM
	PUBLIC.GREEN_TAXI_DATA G
	INNER JOIN PUBLIC.ZONES PUZ ON G."PULocationID" = PUZ."LocationID"
	INNER JOIN PUBLIC.ZONES DOZ ON G."DOLocationID" = DOZ."LocationID"
WHERE
	DATE (LPEP_PICKUP_DATETIME) = '2019-10-18'
GROUP BY
	PUZ."Zone"
HAVING
	SUM(G.TOTAL_AMOUNT) > 13000;
```
## Question 6. Largest tip
For the passengers picked up in Ocrober 2019 in the zone name "East Harlem North" which was the drop off zone that had the largest tip?

Answer: <mark>JFK Airport</mark>

```sql
SELECT
	DOZ."Zone" AS DROPOFF_LOCATION,
	MAX(G.TIP_AMOUNT)
FROM
	PUBLIC.GREEN_TAXI_DATA G
	INNER JOIN PUBLIC.ZONES PUZ ON G."PULocationID" = PUZ."LocationID"
	INNER JOIN PUBLIC.ZONES DOZ ON G."DOLocationID" = DOZ."LocationID"
WHERE
	PUZ."Zone" = 'East Harlem North'
GROUP BY
	1
ORDER BY
	2 DESC;
```
