
# Telecom CDR ETL Pipeline (IICS Project)

## Project Overview
This project implements an end-to-end ETL pipeline for Telecom Call Detail Records (CDR) using Informatica Intelligent Cloud Services (IICS).

The pipeline processes raw telecom data, cleans it, applies transformations, and generates analytical outputs such as call volume, revenue, and international call insights.

---

## Data Sources

1. CDR_RAW_Telecom.csv
   - CallID
   - Caller
   - Receiver
   - Duration
   - CallType
   - TowerID
   - Timestamp

2. Customer_Master_Telecom.csv
   - Phone Number
   - Customer Name
   - Plan Type

3. Tower_Master_Telecom.csv
   - TowerID
   - Region
   - City

---

## Project Architecture

CSV Files
   ↓
Master Data Load (Customer + Tower)
   ↓
CDR Processing (Cleaning + Transformation)
   ↓
CDR_Final Table
   ↓
Analytics Use Cases
   ↓
Reporting Tables

---

## Mappings

### Mapping 1: Tower Master Load
- Source: Tower_Master_Telecom.csv
- Target: Tower_Master
- Purpose: Load tower reference data

---

### Mapping 2: Customer Master Load
- Source: Customer_Master_Telecom.csv
- Transformation:
  - Filter: length(phoneNumber) = 10
- Target: Customer_Master
- Purpose: Load valid customer data

---

### Mapping 3: CDR Processing
- Source: CDR_RAW_Telecom.csv
- Transformations:
  - Convert timestamp to date
  - Remove invalid/future records
  - Replace NULL duration with 0
  - Lookup Customer Master
  - Lookup Tower Master

- Derived Columns:
  - Revenue = Duration * 0.02
  - IsInternational = 1 if CallType = 'INT' else 0

- Target: CDR_Final

---

## Analytical Use Cases

### Use Case 1: Daily Call Volume Summary
- Total Calls
- Total Call Duration
- Average Call Duration
- Calls per Customer

Outputs:
- DailyCallVolume
- CallPerCustomer

---

### Use Case 2: Call Type Performance Analysis
- Total Calls by Call Type
- Total Duration by Call Type
- Revenue by Call Type
- Average Duration per Call Type

Output:
- CallTypePerformance

---

### Use Case 3: International Call Monitoring
- International Call Count
- International Call Duration
- International Revenue
- Percentage of International Calls

Output:
- int_call_monitoring

---

## Final Tables

Dimension Tables:
- Customer_Master
- Tower_Master

Fact Table:
- CDR_Final

Analytical Tables:
- DailyCallVolume
- CallPerCustomer
- CallTypePerformance
- int_call_monitoring

---

## Tools & Technologies
- Informatica Intelligent Cloud Services (IICS)
- Oracle / SQL
- CSV Files

---

## Key Features
- End-to-end ETL pipeline
- Data cleansing and validation
- Lookup and join operations
- Revenue calculation logic
- Multiple analytical use cases

---

## Future Enhancements
- Implement SCD Type 2
- Add audit logging
- Build dashboard (Power BI / Excel)
- Add high usage alerts

---

## Author
Gaurav Katiyar
B.Tech Final Year | Data Engineering
