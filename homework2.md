1. Within the execution for Yellow Taxi data for the year 2020 and month 12: what is the uncompressed file size (i.e. the output file yellow_tripdata_2020-12.csv of the extract task)?
128.3 MB

2. What is the rendered value of the variable file when the inputs taxi is set to green, year is set to 2020, and month is set to 04 during execution?

green_tripdata_2020-04.csv

3. How many rows are there for the Yellow Taxi data for all CSV files in the year 2020?

SELECT SUM(cnt) as total_rows
FROM (
 SELECT COUNT(*) as cnt FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_01_ext` UNION ALL 
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_02_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_03_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_04_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_05_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_06_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_07_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_08_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_09_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_10_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_11_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.yellow_tripdata_2020_12_ext`
);

24,648,499

4. How many rows are there for the Green Taxi data for all CSV files in the year 2020?

SELECT SUM(cnt) as total_rows
FROM (
 SELECT COUNT(*) as cnt FROM `kestrademo.de_zoomcamp.green_tripdata_2020_01_ext` UNION ALL 
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.green_tripdata_2020_02_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.green_tripdata_2020_03_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.green_tripdata_2020_04_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.green_tripdata_2020_05_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.green_tripdata_2020_06_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.green_tripdata_2020_07_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.green_tripdata_2020_08_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.green_tripdata_2020_09_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.green_tripdata_2020_10_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.green_tripdata_2020_11_ext` UNION ALL
 SELECT COUNT(*) FROM `kestrademo.de_zoomcamp.green_tripdata_2020_12_ext`
);

1,734,051

5. How many rows are there for the Yellow Taxi data for the March 2021 CSV file?

SELECT COUNT(*) as rows
FROM `kestrademo.de_zoomcamp.yellow_tripdata_2021_03`

1,925,152


6. How would you configure the timezone to New York in a Schedule trigger?

Add a timezone property set to America/New_York in the Schedule trigger configuration