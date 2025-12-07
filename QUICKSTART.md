# Quick Start Guide

This guide will get you up and running with the data engineering pipeline in under 5 minutes!

## 🚀 Quick Setup (Minimal Dependencies)

### Step 1: Install Python Dependencies
```bash
# Navigate to the project folder
cd data-engineering-pipeline

# Install only the essential dependencies for testing
pip install pandas pyarrow
```

### Step 2: Run the Complete Pipeline
```bash
# Run the simplified ETL pipeline
python simple_etl.py

# Load data into SQLite warehouse
python warehouse/load_data.py
```

That's it! Your pipeline is now running. 🎉

## 📊 Verify the Results

### Check the Database
```bash
# Open SQLite CLI
sqlite3 warehouse/datawarehouse.db

# Run a sample query
SELECT COUNT(*) FROM fact_sales;
.exit
```

### View Example Analytics
```bash
# Open SQLite and run example queries
sqlite3 warehouse/datawarehouse.db
.read warehouse/example_queries.sql
.exit
```

## 📁 What Just Happened?

1. **ETL Pipeline** (`simple_etl.py`):
   - Loaded sample data (1,000 sales transactions)
   - Cleaned and transformed data
   - Created fact and dimension tables
   - Saved to `datalake/warehouse/` as Parquet files

2. **Warehouse Loading** (`warehouse/load_data.py`):
   - Created SQLite database
   - Loaded Parquet files into tables
   - Verified data integrity

## 🔍 Explore Your Data

### Data Lake Zones
- **`datalake/raw/`** - Original CSV/JSON files
- **`datalake/staging/`** - Validated copies
- **`datalake/processed/`** - Enriched fact table (Parquet)
- **`datalake/warehouse/`** - Dimension tables (Parquet)

### Database Tables
- **`fact_sales`** - 1,000 sales transactions
- **`dim_products`** - 50 products across 6 categories
- **`dim_customers`** - 100 customers across 5 regions

## 📈 Next Steps

### Option 1: Explore with SQL
Run the example queries in `warehouse/example_queries.sql`:
- Top products by revenue
- Customer lifetime value
- Daily revenue trends
- Regional analysis

### Option 2: Set Up Apache Airflow (Advanced)
```bash
# Install Airflow
pip install apache-airflow==2.8.0

# Initialize Airflow
export AIRFLOW_HOME=$(pwd)  # Windows: set AIRFLOW_HOME=%cd%
airflow db init

# Create admin user
airflow users create \
    --username admin \
    --password admin \
    --firstname Admin \
    --lastname User \
    --role Admin \
    --email admin@example.com

# Start services (in separate terminals)
airflow webserver -p 8080
airflow scheduler

# Access UI: http://localhost:8080
```

### Option 3: Set Up Apache Superset (Advanced)
```bash
# Install Superset
pip install apache-superset==3.1.0

# Follow the detailed guide
See: superset/superset_setup.md
```

### Option 4: Use Full Spark Pipeline (Advanced)
```bash
# Install Java 8+ and PySpark
pip install pyspark==3.5.0

# Run the full Spark ETL
python spark/etl_job.py
```

## 🛠️ Customization

### Add Your Own Data
Replace the sample data files in `datalake/raw/`:
- `sales.csv` - Your transaction data
- `products.json` - Your product catalog
- `customers.csv` - Your customer information

Then re-run the pipeline:
```bash
python simple_etl.py
python warehouse/load_data.py
```

### Modify Transformations
Edit `simple_etl.py` or `spark/etl_job.py` to:
- Add new calculated columns
- Create additional aggregations
- Implement custom business logic

## 📚 Documentation

- **README.md** - Complete documentation
- **superset/superset_setup.md** - Dashboard setup
- **warehouse/example_queries.sql** - SQL examples

## 🔧 Troubleshooting

### Issue: Module not found
```bash
# Install missing dependency
pip install [module-name]
```

### Issue: Database file not found
```bash
# Make sure you ran both scripts
python simple_etl.py
python warehouse/load_data.py
```

### Issue: Permission errors
```bash
# Make sure you're in the project directory
cd data-engineering-pipeline
```

## 💡 Tips

1. **Start Simple**: Use `simple_etl.py` for testing without Spark
2. **Incremental**: Add Airflow/Superset only when needed
3. **Explore**: Modify SQL queries to understand your data
4. **Learn**: Read through the code to understand ETL concepts

---

**Happy Data Engineering! 🚀**
