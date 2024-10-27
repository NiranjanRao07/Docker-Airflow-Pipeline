# Yfinance to Snowflake ETL

This project leverages **Apache Airflow** in **Google Cloud Composer** to automate the ETL pipeline for loading **Yahoo Finance** stock data into **Snowflake**. Each day, stock data is extracted for a specified symbol, transformed, and loaded into a Snowflake table, enabling easy access for analytics and reporting.

---

## 📖 About

This Airflow DAG extracts daily stock data for a given symbol (e.g., `AAPL`) from Yahoo Finance and loads it into Snowflake for further analysis. The data is stored in the `stock_data_db.raw_data.yfinance` table, with fields for date, open, close, high, low, volume, and symbol.

---

## 🚀 Setup and Usage

1. **Dependencies**: Ensure `apache-airflow-providers-snowflake` is added to your **Cloud Composer** environment’s PyPI packages.

2. **Airflow Variables and Connections**:
   - Create a Snowflake connection in Airflow (`snowflake_conn`) with the necessary credentials.

3. **DAG Structure**:
   - `extract`: Extracts stock data for a specific date from Yahoo Finance using the `yfinance` library.
   - `load`: Loads the extracted data into Snowflake, creating the target table if it doesn't exist.

4. **Trigger the DAG**: 
   - The DAG runs daily at 02:05 UTC to load the previous day’s stock data.

---

## 🔧 Key Functions

- **get_next_day**: Helper function to calculate the next day’s date.
- **return_snowflake_conn**: Establishes and returns a Snowflake connection.
- **extract**: Extracts stock data for a specific date.
- **load**: Creates or updates the Snowflake table with the extracted stock data.

---

## 📅 Schedule

- **Cron Schedule**: `5 2 * * *` (Runs daily at 02:05 UTC).

---

## Example

Run the `YfinanceToSnowflake` DAG in Cloud Composer to automate daily stock data ETL from Yahoo Finance to Snowflake.
