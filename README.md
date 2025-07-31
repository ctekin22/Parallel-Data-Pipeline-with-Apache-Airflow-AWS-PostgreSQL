# Parallel Data Ingestion Pipeline using Apache Airflow, AWS, PostgreSQL
This project ingests weather data from the OpenWeatherMap API and store data from a CSV in S3, processes them in parallel, loads them into AWS RDS PostgreSQL, joins both datasets, and writes the result back to S3. The entire pipeline is orchestrated using Apache Airflow.

- **Apache Airflow** (deployed on EC2)
- **AWS S3**
- **PostgreSQL (Amazon RDS)**
- **OpenWeatherMap API**


---

## 📌 Features

- 🔄 Parallel task execution with **TaskGroups**
- 🐘 PostgreSQL ingestion using `PostgresOperator`
- 🌐 HTTP API consumption using `HttpSensor` & `SimpleHttpOperator`
- 🧠 Python transformations via `PythonOperator`
- 🔁 Inter-task communication with **XCom**
- ☁️ AWS S3 read/write with `boto3` and `s3fs`
- 🧩 Modular, extensible Airflow DAG
- 🖥️ Fully hosted on an EC2 instance

---

## 🗂️ Project Structure

```
├── scripts/airflow/dags/
│   └── weather_dag.py         # Main DAG with TaskGroups and logic
├── plugins/
│   └── custom_operators/      # Optional: for custom logic
├── datasets/
│   └── cities.csv             # Sample CSV file in S3
├── docs          
└── README.md                  # This file
```

---

## 🛠️ Tools & Technologies

| Tool            | Purpose                                 |
|-----------------|------------------------------------------|
| Apache Airflow  | Orchestration of ETL tasks              |
| AWS S3          | Raw and cleaned data storage            |
| AWS EC2         | Hosting Airflow                         |
| AWS RDS         | PostgreSQL database for data warehouse  |
| OpenWeatherMap  | Weather API                             |
| PostgreSQL      | Final structured data storage           |
| Python          | Transformations                         |
| `boto3`         | AWS S3 interaction                      |

---

## ⚙️ Pipeline Overview

### 🧩 TaskGroup 1: Weather Data Ingestion
- Get current weather using OpenWeatherMap API (via HTTPOperator)
- Transform JSON using `PythonOperator`
- Load to PostgreSQL

### 🧩 TaskGroup 2: S3 CSV Ingestion
- Download CSV from S3 using `boto3`
- Transform using `pandas`
- Load to PostgreSQL

### ✅ Final Task
- Join weather and CSV data in PostgreSQL
- Export final DataFrame to cleaned CSV
- Upload result back to S3

---

## 🔐 Environment Variables

Set these in your `.env` or Airflow connection manager:

```env
AWS_ACCESS_KEY_ID=your_key
AWS_SECRET_ACCESS_KEY=your_secret
OPENWEATHERMAP_API_KEY=your_weather_api_key
POSTGRES_CONN_ID=your_airflow_postgres_connection_id
S3_BUCKET_NAME=your-s3-bucket-name
```

---

## 🚀 How to Run

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/airflow-weather-pipeline.git
cd airflow-weather-pipeline
```

### 2. Set Up Airflow on EC2
Create and activate a virtual environment:
```bash
python3 -m venv airflow_venv
source airflow_venv/bin/activate
pip install -r requirements.txt
```

### 3. Place Your DAG
Copy `weather_dag.py` into your `~/airflow/dags/` folder.

### 4. Trigger the DAG
Visit Airflow UI at `http://your-ec2-ip:8080`, turn on the `weather_dag`.

---

## 📊 Example Use Case

Imagine you want to analyze how **weather patterns** affect **electricity usage** in various cities. You can extend this pipeline to include:
- Historical weather data
- Power grid data
- Machine learning predictions on power consumption

---




   
