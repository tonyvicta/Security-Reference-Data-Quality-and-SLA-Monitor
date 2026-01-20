# Security Reference Data Mini Project

## Overview
I built a small security reference data pipeline that mirrors how an Investment Data Services team supports daily operations. The project ingests Bloomberg style security attributes plus a secondary vendor snapshot, validates and profiles the data, integrates it into a single internal Security Master record, manages exceptions with SLA tracking, and distributes curated tables to Power BI for reporting.

All datasets in this repo are synthetic and created for interview preparation.

## Objective
Build a small security reference data pipeline that ingests Bloomberg style security attributes, validates them, integrates them into a single internal Security Master record, manages exceptions with SLA tracking, and distributes a curated dataset to Power BI for reporting.

## Workflow and tasks

### Step 1 Sourcing
Project task  
Load daily security reference extracts from Bloomberg plus one secondary vendor into landing tables.

What I demonstrate  
I understand vendor sourcing, field formats, and the idea that different vendors can disagree.

Bloomberg angle  
Includes Bloomberg identifiers and fields such as BBGID, FIGI, Ticker, Yellow Key, ID_ISIN, ID_CUSIP, ID_SEDOL1, CRNCY, EXCH_CODE, SECURITY_TYP, MATURITY, CPN, DAY_CNT_DES.

### Step 2 Analysis
Project task  
Run data quality checks and profiling.

Checks included  
1. Completeness for key identifiers  
2. Duplicate detection on ISIN and BBGID  
3. Cross field validation such as currency versus exchange region  
4. Freshness check using LastUpdated  
5. Outlier checks for coupon and maturity on bonds  

### Step 3 Integration
Project task  
Create an internal golden record Security Master.

Rule examples  
1. Prefer Bloomberg for identifiers and descriptive fields  
2. Prefer secondary vendor for missing attributes when Bloomberg is blank  
3. Standardise exchange codes and currency codes  
4. Create one internal SecurityID per instrument  

### Step 4 Management
Project task  
Create an exception queue and track investigation outcomes.

What I track  
Issue type, root cause, resolution method, escalations, SLA due date, reopen flag.

### Step 5 Distribution
Project task  
Publish curated tables and build a Power BI report.

Power BI pages  
1. Data Quality Overview  
2. Exceptions and SLA  
3. Vendor Comparison  
4. Index and Portfolio Impact  

## Deliverables
1. Clean Security Master table  
2. Vendor comparison table  
3. Exception queue table with SLA measures  
4. Power BI report built on those tables  

## Repository structure
Suggested structure for this repo

* data  
  * DimSecurityMaster.csv  
  * FactVendorSecuritySnapshot.csv  
  * FactExceptions.csv  
  * FactIndexConstituents.csv  
  * FactPortfolioHoldings.csv  
* docs  
  * ProjectTasks.md  
  * PowerBI_Measures_DAX.txt  
* screenshots  
  * Optional screenshots of the Power BI pages  
* README.md  

## How to use in Power BI
1. Open Power BI Desktop  
2. Get Data then Text or CSV and load each file from the data folder  
3. Create relationships using SecurityID as the key  
4. Build the pages listed above  
5. Add measures for SLA performance, time to resolve, aging buckets, reopen rate  

## Notes on realism
This project is intentionally designed to reflect common reference data challenges:
* Vendor mismatches for the same field  
* Exchange code mapping differences  
* Currency code differences at share class level  
* Exceptions that require triage, investigation, documentation, and escalation  

## Tech stack used
* CSV as a simple landing format for vendor snapshots  
* Power BI for reporting and operational monitoring  
* SQL and Python are natural next steps to automate the checks and integration logic  

## Future enhancements
1. Add a small data dictionary for each table and field  
2. Add automated validation rules and exception generation logic in SQL or Python  
3. Add a simple audit log that captures who changed what and when  
4. Add refresh scheduling and alerting based on SLA breach risk  

## Disclaimer
All data in this repository is synthetic and for demonstration purposes only.
