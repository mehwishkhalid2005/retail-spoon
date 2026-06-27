# retail-spoon
This repository features an end-to-end data engineering and business intelligence pipeline. The system automates the workflow of extracting raw operational transaction records from a relational database, processing the data via an automation script, and surfacing actionable corporate insights through a polished dashboard.
## 🚀 System Architecture & Workflow

1. **Relational Database (PostgreSQL):** Hosts a normalized star schema utilizing explicit primary and foreign key constraints to link `sales` transaction facts with `customers` and `products` dimensions.
2. **Automated ETL (Python):** A script leverages `psycopg2` to establish secure database connectivity and runs optimized queries. The resulting dataset is loaded into a `pandas` DataFrame for transformation and exported to a production-ready file (`clean_retail_sales.csv`).
3. **Business Intelligence (Power BI):** A tracking dashboard that ingests the processed data layer to display core corporate metrics—featuring a high-level revenue KPI card, regional market distribution (UAE, USA, UK), and product performance rankings.

---

## 📊 Dashboard Preview
[Executive Sales Dashboard](Screenshot 2026-06-23 221944.png)

---

## 💻 Core Extraction Query

The extraction layer relies on the following relational SQL join structure:

```sql
SELECT 
    s.sale_id, 
    s.sale_date, 
    s.quantity, 
    s.total_amount,
    c.customer_name, 
    c.country,
    p.product_name, 
    p.category, 
    p.price
FROM sales s
JOIN customers c ON s.customer_id = c.customer_id
JOIN products p ON s.product_id = p.product_id;
```

---

## 🛠️ How to Execute Locally

### 1. Database Initialization
Execute the `schema.sql` script inside your local PostgreSQL database instance to build and seed the relational tables:
```sql
-- Run your schema script to create tables and insert seed data
\i schema.sql
```

### 2. Environment Setup & Dependencies
Install the required Python data engineering packages within your terminal:
```bash
pip install pandas psycopg2-binary
```

### 3. Run the ETL Pipeline
Configure your local database credentials inside `pipeline.py` and execute the script to generate the data layer:
```bash
python pipeline.py
```

### 4. Open the Analytics Layer
Launch Power BI Desktop and open `Retail_Analysis.pbix` to interact with the visualizations.
