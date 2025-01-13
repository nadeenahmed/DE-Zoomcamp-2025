## Question 3. Count records
How many taxi trips were made on October 18th, 2019?

(Trips that started and finished on that day)

answer: 17417
```sql
SELECT
	COUNT(*)
FROM
	PUBLIC.GREEN_TAXI_DATA
WHERE
	DATE (LPEP_PICKUP_DATETIME) = '2019-10-18'
	AND DATE (LPEP_DROPOFF_DATETIME) = '2019-10-18'
```
