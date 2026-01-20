# Security reference data mini project

## Purpose
This mini project mirrors how an investment data services team handles security reference data.
You ingest vendor snapshots, validate quality, integrate a golden security master record, manage exceptions with SLA tracking, then visualise results in Power BI.

All data in this repo is synthetic.

## Data tables
All files live in the data folder.

1. DimSecurityMaster.csv, internal security master record with identifiers and Bloomberg style fields.
2. FactVendorSecuritySnapshot.csv, vendor snapshots from Bloomberg and Refinitiv stored one field per row, with intentional conflicts.
3. FactExceptions.csv, exception queue with SLA dates, root cause, and resolution method.
4. FactIndexConstituents.csv, sample index membership and weights.
5. FactPortfolioHoldings.csv, sample holdings used to show impact.

## Docs
The docs folder contains

1. ProjectTasks.md, the five step workflow and deliverables
2. PowerBI_Measures_DAX.txt, a few simple measures you can copy into Power BI

## Power BI quick build
1. Open Power BI Desktop
2. Get Data, Text CSV, load all five tables from the data folder
3. Create relationships using SecurityID from DimSecurityMaster to each fact table
4. Add measures from docs PowerBI_Measures_DAX.txt
5. Build visuals for exceptions, SLA performance, and vendor mismatches

## Bloomberg knowledge you can talk to
The dataset includes Bloomberg style identifiers and fields such as BBGID, FIGI, YellowKey, and vendor attributes like ID_ISIN, CRNCY, EXCH_CODE, MATURITY, CPN, and DAY_CNT_DES.

## Publish this folder to GitHub
From a terminal in the project folder

1. git init
2. git add .
3. git commit
4. Create a new repository in GitHub and copy the repository URL
5. git remote add origin YOUR_REPO_URL
6. git push origin master
