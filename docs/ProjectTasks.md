# Project Tasks
Security Reference Data Mini Project

## Purpose
This mini project simulates how an Investment Data Services team handles security reference data from vendor sourcing through to operational distribution. It focuses on data quality controls, exception handling with SLA tracking, and delivery into Power BI for monitoring.

All data is synthetic and created for demonstration only.

## Setup
1. Create a repo with folders
   • data  
   • docs  
   • screenshots  

2. Add these CSV files into the data folder
   
   • DimSecurityMaster.csv  
   • FactVendorSecuritySnapshot.csv  
   • FactExceptions.csv  
   • FactIndexConstituents.csv  
   • FactPortfolioHoldings.csv  

4. Open Power BI Desktop and load all CSV files from the data folder.

5. In Power Query, set data types
   • Dates: CreatedDate, DueDate, ClosedDate, AsOfDate, MaturityDate, LastUpdated  
   • Numbers: Coupon, Weight, Quantity, LocalPrice, MarketValueLocal, MarketValueBase, SLAHours  
   • Text: everything else

6. Build relationships in the data model
   • DimSecurityMaster[SecurityID] to FactExceptions[SecurityID]  
   • DimSecurityMaster[SecurityID] to FactVendorSecuritySnapshot[SecurityID]  
   • DimSecurityMaster[SecurityID] to FactIndexConstituents[SecurityID]  
   • DimSecurityMaster[SecurityID] to FactPortfolioHoldings[SecurityID]  

## Step 1 Sourcing
Goal
Load daily security reference extracts from Bloomberg style attributes plus a secondary vendor snapshot.

Tasks
1. Treat FactVendorSecuritySnapshot as the landing table for vendor snapshots.
2. Confirm the dataset includes Bloomberg style fields such as
   • BBGID  
   • FIGI  
   • Ticker  
   • YellowKey  
   • ID_ISIN  
   • ID_CUSIP  
   • ID_SEDOL1  
   • CRNCY  
   • EXCH_CODE  
   • SECURITY_TYP  
   • MATURITY  
   • CPN  
   • DAY_CNT_DES  

Outcome
You can explain how vendor feeds arrive daily, why formats differ, and how conflicts occur.

## Step 2 Analysis
Goal
Run data quality checks and profiling.

Tasks
1. Completeness checks
   • ISIN present for most assets where applicable  
   • BBGID present for Bloomberg sourced records  
   • Currency present for all securities  
   • MaturityDate and Coupon present for bonds  

2. Duplicate checks
   • Duplicate ISIN across SecurityID  
   • Duplicate BBGID across SecurityID  

3. Cross field validation
   • Currency and exchange combinations make sense for region  
   • AssetClass aligns with YellowKey or SECURITY_TYP expectations  

4. Freshness check
   • Flag records where LastUpdated is older than a defined threshold

5. Outlier checks for bonds
   • Coupon outside a realistic range  
   • MaturityDate missing or earlier than CreatedDate

Outcome
You can describe how exceptions are discovered through automated rules and user tickets.

## Step 3 Integration
Goal
Create an internal golden record Security Master.

Tasks
1. Use DimSecurityMaster as the golden record table.
2. Define clear field precedence rules
   • Prefer Bloomberg for identifiers and descriptive fields  
   • Use secondary vendor to fill blanks when Bloomberg is missing  
   • Standardise exchange codes and currency codes  
   • Maintain a single internal SecurityID per instrument  

3. Create a vendor comparison view in Power BI
   • Use FactVendorSecuritySnapshot to show the same field from two vendors side by side
   • Highlight mismatches for investigation

Outcome
You can explain how a security master consolidates multiple vendors into one trusted internal record.

## Step 4 Management
Goal
Create an exception queue and track investigation outcomes with SLA.

Tasks
1. Use FactExceptions as the operational exception queue.
2. Track and report on
   • IssueType  
   • FieldImpacted  
   • RootCause  
   • ResolutionMethod  
   • EscalatedFlag  
   • ReopenedFlag  
   • SLA due dates and breach flags  

3. Add operational triage logic in the report
   • High priority and due today at the top  
   • Aging buckets for open items  
   • Reopen rate to identify unstable fixes  

Outcome
You can describe how work is prioritised, escalated, and closed within SLA.

## Step 5 Distribution
Goal
Publish curated tables and build a Power BI report that supports daily operations.

Report pages
1. Data Quality Overview
   • Open exceptions  
   • SLA met percent  
   • Average time to resolve  
   • Exceptions trend  

2. Exceptions and SLA
   • Aging buckets  
   • Due today list  
   • SLA breach list  
   • Reopened items  

3. Vendor Comparison
   • Mismatches by VendorField  
   • Mismatches by vendor  
   • Drill to SecurityID and impacted fields  

4. Index and Portfolio Impact
   • Top indices by impacted constituents  
   • Portfolio holdings tied to open exceptions  
   • Market value exposure to open issues  

Outcome
You can explain how curated data supports investment decisions and operational risk control.

## Interview talking points
1. How vendor differences create operational risk and how you control it.
2. How you investigate a mismatch, identify root cause, and prevent recurrence.
3. How SLA and prioritisation decisions are made.
4. How Power BI supports daily queue management and process improvement.
