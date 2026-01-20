# Project tasks aligned to the five step workflow

## Step 1 Sourcing
1. Treat FactVendorSecuritySnapshot.csv as the vendor landing feed.
2. Confirm you understand the vendor naming and fields, for example Bloomberg fields like ID_ISIN, CRNCY, EXCH_CODE, MATURITY, CPN, DAY_CNT_DES.

## Step 2 Analysis
1. Profile completeness for key identifiers, ISIN, CUSIP, SEDOL, BBGID.
2. Identify vendor mismatches using FactVendorSecuritySnapshot.csv, for example coupon mismatches on bonds and currency code conflicts on funds.
3. Identify freshness issues using DimSecurityMaster LastUpdated.

## Step 3 Integration
1. Use DimSecurityMaster.csv as the golden record.
2. Explain how you would choose a preferred source by field, and how you would fall back to a secondary vendor when a value is missing.
3. Document any mapping tables you would need, for example exchange code mapping.

## Step 4 Management
1. Use FactExceptions.csv as the exception queue.
2. Track SLA performance, aging, escalations, and reopen flags.
3. For each open exception, state the investigation path, what you would check first, what evidence you would gather, and when you would escalate.

## Step 5 Distribution
1. Load the tables into Power BI.
2. Build a one page dashboard that answers, what is the queue health, what is driving SLA misses, and which vendors cause the most exceptions.
3. Add an impact view using holdings or index membership to show why reference data issues matter.
