# Parallel-Data-Pipeline-with-Apache-Airflow-AWS-PostgreSQL
This project ingests weather data from the OpenWeatherMap API and store data from a CSV in S3, processes them in parallel, loads them into AWS RDS PostgreSQL, joins both datasets, and writes the result back to S3. The entire pipeline is orchestrated using Apache Airflow.
