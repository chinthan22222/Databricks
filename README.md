# HR Data Engineering Pipeline (Databricks + PySpark)

## Project Overview
This project implements an end-to-end data engineering pipeline using PySpark on Databricks. It follows the Medallion Architecture (Bronze → Silver → Gold) to process raw HR data from multiple sources, perform transformations, enrich data through joins, and generate business-ready outputs.

---

## Objective
To design and build a scalable data pipeline that:
- Ingests data from CSV, JSON, and Parquet formats  
- Cleans and transforms raw datasets  
- Enriches data using joins  
- Performs analytical queries  
- Stores final outputs for reporting  

---

## Architecture

Raw Data → Bronze → Silver → Gold

### Bronze Layer (Raw Data)
- Employees (CSV)  
- Departments (JSON)  
- Salary Bands (CSV)  
- New Hires (Parquet)  

### Silver Layer (Processed Data)
- employees_clean (cleaned and transformed employee data)
- new_hires_clean (cleaned and transformed new hires data)
- employees_all_clean (cleaned and transformed employee + new hired data)

### Gold Layer (Business Outputs)
- final_report & employees_gold (fully enriched employee dataset)  
- dept_summary (aggregated department metrics)  
- partitioned_report (final data partitioned by department)

---

## Project Structure

```text
Databricks/
└── hr_project/
    ├── notebooks/
    │   ├── 01_data_ingestion.ipynb    
    │   ├── 02_data_cleaning.ipynb      
    │   ├── 03_business_logic.ipynb
    |   ├── 04_joins
    |   ├── 05_analysis
    |   ├── 06_union 
    │   └── 07_output.ipynb      
    └── data/                       
```
---

## Pipeline Phases

### Phase 1: Data Setup
- Define data paths  
- Validate file availability  

### Phase 2: Ingestion
- Read CSV, JSON, and Parquet data  
- Validate schema consistency  

### Phase 3: Transformation
- Convert join_date to DateType  
- Add derived columns:
  - experience_level  
  - days_employed  
  - salary_band  
- Filter active employees  
- Rename dept to department  
- Drop unnecessary columns  

### Phase 4: Data Enrichment (Joins)
- Inner join with departments  
- Left join to find unmatched departments  
- Anti join to detect departments with no employees  
- Multi-key join (dept and gender) with salary bands  
- Self join to find employee pairs in the same department  

### Phase 5: Business Analysis
- Top 3 highest-paid employees (SQL)  
- Departments with average salary above threshold  
- Department-level aggregation (headcount, average salary, total bonus)  

### Phase 6: Data Integration
- Union employees with new hires  
- Re-apply transformations  
- Enrich final dataset with department information  

### Phase 7: Output
- Save final report as Parquet  
- Save department summary as CSV  
- Partition final dataset by department  
- Validate saved outputs  

---

## Technologies Used
- Databricks  
- PySpark  
- Spark SQL  
- Parquet  
- Unity Catalog (Volumes)  

---

## Key Features
- End-to-end ETL pipeline  
- Multi-format data ingestion  
- Advanced join operations  
- Feature engineering  
- SQL-based analytics  
- Partitioned data storage  
- Modular pipeline design  

---


