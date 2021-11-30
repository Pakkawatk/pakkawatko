[<<Home](https://pakkawatk.github.io/portfolio)<br />
# Google Cloud Platform Projects.
This page briefly demonstates my GCP projects while I'm studying at DPU.<br />
### Creating Data Warehouse in Google Cloud Platform.
**Dataset:** PUB/SUB Taxi Rider dataset.<br />
**Objective:** Monitor business in real-time with streaming data pipeline that capture taxi revenue, passenger count, ride status.<br />
**Process:**<br />
- Create Project, Pub/Sub BigQuery dataset and Schema.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/gcp1.PNG?raw=true)<br /><br />
- Create Cloud Storage Bucket.
- Set up Dataflow Pipeline from Template.<br />
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/gcp0.PNG?raw=true)<br /><br />
- Query and aggreate data<br />

```

WITH streaming_data AS (
SELECTtimestamp,
  TIMESTAMP_TRUNC(timestamp, HOUR, 'UTC') AS hour,
  TIMESTAMP_TRUNC(timestamp, MINUTE, 'UTC') AS minute,
  TIMESTAMP_TRUNC(timestamp, SECOND, 'UTC') AS second,
  ride_id,
  latitude,
  longitude,
  eter_reading,
  ride_status,
  passenger_count
FROM
  taxirides.realtime
WHERE ride_status = 'dropoff' 
ORDER BY timestamp DESC
LIMIT 100000
)

# calculate aggregations on stream for reporting:
SELECT
  ROW_NUMBER() OVER() AS dashboard_sort,minute,
  COUNT(DISTINCT ride_id) AS total_rides,
  SUM(meter_reading) AS total_revenue,SUM(passenger_count) AS total_passengers
FROM streaming_data
GROUP BY minute, timestamp

```

![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/gcp2.PNG?raw=true)<br /><br />
- Create Real Time Visualization over timestamp.
![Image](https://github.com/Pakkawatk/portfolio/blob/gh-pages/img/gcp3.PNG?raw=true)<br /><br />

[<<Home](https://pakkawatk.github.io/portfolio)<br />
