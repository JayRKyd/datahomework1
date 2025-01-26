Question 1. Understanding docker first run
Run docker with the python:3.12.8 image in an interactive mode, use the entrypoint bash.

What's the version of pip in the image?

Answer: 
root@1242861ac6c3:/# pip --version
pip 24.3.1 from /usr/local/lib/python3.12/site-packages/pip (python 3.12)


Question 2. Understanding Docker networking and docker-compose
Given the following docker-compose.yaml, what is the hostname and port that pgadmin should use to connect to the postgres database?

services:
  db:
    container_name: postgres
    image: postgres:17-alpine
    environment:
      POSTGRES_USER: 'postgres'
      POSTGRES_PASSWORD: 'postgres'
      POSTGRES_DB: 'ny_taxi'
    ports:
      - '5433:5432'
    volumes:
      - vol-pgdata:/var/lib/postgresql/data

  pgadmin:
    container_name: pgadmin
    image: dpage/pgadmin4:latest
    environment:
      PGADMIN_DEFAULT_EMAIL: "pgadmin@pgadmin.com"
      PGADMIN_DEFAULT_PASSWORD: "pgadmin"
    ports:
      - "8080:80"
    volumes:
      - vol-pgadmin_data:/var/lib/pgadmin  

volumes:
  vol-pgdata:
    name: vol-pgdata
  vol-pgadmin_data:
    name: vol-pgadmin_data

Answer:
postgres:5432



Question 3. Trip Segmentation Count
During the period of October 1st 2019 (inclusive) and November 1st 2019 (exclusive), how many trips, respectively, happened:

Up to 1 mile
In between 1 (exclusive) and 3 miles (inclusive),
In between 3 (exclusive) and 7 miles (inclusive),
In between 7 (exclusive) and 10 miles (inclusive),
Over 10 miles

104,802 197,670 110,612 27,831 35,281

Question 4. Longest trip for each day
Which was the pick up day with the longest trip distance? Use the pick up time for your calculations.

Tip: For every day, we only care about one single trip with the longest distance.

Answer:
SELECT 
    DATE(lpep_pickup_datetime) AS pickup_date,
    MAX(trip_distance) AS max_distance
FROM green_taxi_data
GROUP BY pickup_date
ORDER BY max_distance DESC
LIMIT 1;

"2019-10-31"	515.89

Question 5. Three biggest pickup zones
Which were the top pickup locations with over 13,000 in total_amount (across all trips) for 2019-10-18?

Consider only lpep_pickup_datetime when filtering by date.

Answer: 
SELECT 
    z."Borough",
    z."Zone" as zone_name,
    SUM(gtd."total_amount") AS total_amount
FROM green_taxi_data gtd
LEFT JOIN zones z ON gtd."PULocationID" = z."LocationID"
WHERE DATE(gtd."lpep_pickup_datetime") = '2019-10-18'
GROUP BY z."Borough", z."Zone"
HAVING SUM(gtd."total_amount") > 13000
ORDER BY total_amount DESC;

Answer:
East Harlem North, East Harlem South, Morningside Heights



Question 6. Largest tip
For the passengers picked up in October 2019 in the zone named "East Harlem North" which was the drop off zone that had the largest tip?

SELECT 
   dropoff_zone."Zone" as dropoff_zone,
   MAX(gtd."tip_amount") as max_tip
FROM green_taxi_data gtd
JOIN zones pickup_zone 
   ON gtd."PULocationID" = pickup_zone."LocationID"
JOIN zones dropoff_zone 
   ON gtd."DOLocationID" = dropoff_zone."LocationID"
WHERE 
   pickup_zone."Zone" = 'East Harlem North'
   AND gtd."lpep_pickup_datetime"::date BETWEEN '2019-10-01' AND '2019-10-31'
GROUP BY dropoff_zone."Zone"
ORDER BY max_tip DESC
LIMIT 1;

Answer: 
"JFK Airport"	87.3



Question 7. Terraform Workflow
Which of the following sequences, respectively, describes the workflow for:

Downloading the provider plugins and setting up backend,
Generating proposed changes and auto-executing the plan
Remove all resources managed by terraform`

Answer: 
terraform init, terraform apply -auto-approve, terraform destroy