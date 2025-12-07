#  On-Premise Data Lake with Apache Spark ETL, Apache Airflow Orchestration & Apache Superset Dashboards



## ✨ Project Summary

This repository contains a **complete on-premise data engineering pipeline** built to simulate a production-like enterprise workflow on a local machine (no cloud required). The stack demonstrates ingestion, ETL, orchestration, warehousing, and BI visualization using open-source tooling.

Key components:

* Local Data Lake (raw / staging / processed)
* Apache Spark (PySpark) ETL
* Apache Airflow DAG-based orchestration
* Local warehouse (Parquet / SQLite / optional PostgreSQL)
* Apache Superset dashboards for analytics

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## 🏗 System Architecture (visual)

```
                      ┌──────────────────────┐
                      │     Data Sources      │
                      │  CSV / JSON / APIs    │
                      └─────────┬────────────┘
                                │
                                ▼
                  ┌─────────────────────────────┐
                  │     On-Premise Data Lake     │
                  │  raw / staging / processed   │
                  └──────────┬───────────────────┘
                             │
                             ▼
          ┌──────────────────────────────────────────┐
          │         Apache Airflow (Scheduler)        │
          │  Triggers Spark ETL on schedule           │
          └──────────┬───────────────────────────────┘
                     │
                     ▼
          ┌──────────────────────────────────────────┐
          │           Apache Spark ETL Pipeline       │
          │   Cleaning | Transforming | Aggregations  │
          └──────────┬───────────────────────────────┘
                     │
                     ▼
   ┌───────────────────────────────────────────────────────────┐
   │    Local Data Warehouse (Parquet / SQLite / PostgreSQL)   │
   └──────────┬────────────────────────────────────────────────┘
              │
              ▼
     ┌───────────────────────────────────────┐
     │         Apache Superset           │
     │     Dashboards & Visual Analytics │
     └───────────────────────────────────┘
```

### ETL Pipeline Implementation

![Apache Spark ETL Pipeline](elt.png)

---

## 📂 Data Lake Structure

```
datalake/
    ├── raw/
    │     ├── sales.csv
    │     ├── products.json
    │     ├── customers.csv
    ├── staging/
    ├── processed/
    └── warehouse/
```

### Data Warehouse Structure

![Data Warehouse Implementation](warehouse.png)

---


## 🧰 Built With

**Storage**

* Local File System (Data Lake)

**Processing**

* Apache Spark (PySpark)

**Workflow Orchestration**

* Apache Airflow (DAGs)

**Analytics**

* Apache Superset

**Warehouse**

* Parquet
* SQLite / (PostgreSQL optional)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## 🔧 Workflow (detailed)

### 1️⃣ Data Ingestion — Raw Zone

Sources include CSV, JSON and optional API exports. Dropped into `datalake/raw/` for automated pick-up.

### 2️⃣ Apache Airflow DAG — Pipeline Automation

Airflow does the orchestration (ingest → ETL → validate → load → refresh). Example DAG snippet:

```python
with DAG('spark_etl_pipeline', schedule_interval='@daily') as dag:

    ingest = BashOperator(...)
    spark_etl = SparkSubmitOperator(...)
    validate = PythonOperator(...)
    load_warehouse = BashOperator(...)
```

### 3️⃣ Apache Spark ETL — Transform Phase

Spark performs null/anomaly removal, type conversions, feature engineering, joins, aggregations and writes parquet output to `/processed` and analytics-ready tables to `/warehouse`.

Example:

```python
df = spark.read.csv("datalake/raw/sales.csv", header=True, inferSchema=True)
cleaned = df.dropna().withColumn("total", df.qty * df.price)
cleaned.write.mode("overwrite").parquet("datalake/processed/sales")
```

### 4️⃣ Data Warehouse — Load Phase

Processed datasets are stored as parquet files or optionally as SQL tables (SQLite/Postgres) for Superset connectivity.

### 5️⃣ Apache Superset — Dashboard Layer

Typical dashboards:

* Revenue by month
* Sales trend analysis
* Region-wise sales map
* Top products by revenue
* Customer distribution by location
* Return/Refund analysis

![Apache Superset Dashboard](dashboard.png)

---

## 🎯 Final Deliverables

* ✅ Complete On-Prem Data Lake
* ✅ Spark ETL PySpark Scripts
* ✅ Airflow DAG (scheduler + operators)
* ✅ Structured Warehouse (Parquet / SQL)
* ✅ Superset Dashboards (6–10 charts)
* ✅ Architecture Diagram + Documentation

---

## 🚀 Quick Start — Add this README to your repository

> **Important:** The steps below will initialize a git repo locally and push **only** to your personal branch. **Do not push to `main`**.

```bash
# Initialize a new Git repository (if not initialized)
git init

# Add all project files
git add .

# Add remote GitHub repository (one-time)
git remote add origin https://github.com/rv-ethereal/Data_Mining_LAB.git

# Commit your changes
git commit -m "msa24021 repo push"

# Create and switch to your own branch (replace with your enrollment number)
git checkout -b msa24021

# Push ONLY to your own branch — NOT to main
git push origin msa24021
```

> If `origin` already exists and you need to update it, run:

```bash
git remote set-url origin https://github.com/rv-ethereal/Data_Mining_LAB.git
```

---





**Repository:** [https://github.com/rv-ethereal/Data_Mining_LAB](https://github.com/rv-ethereal/Data_Mining_LAB)

---

<p align="right">(<a href="#readme-top">back to top</a>)</p>
