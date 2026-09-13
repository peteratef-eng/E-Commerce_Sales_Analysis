# E-Commerce Sales Analysis

Exploratory data analysis of transactional data from a UK-based online retailer, using Python and Pandas to evaluate sales performance, cancellations/returns, product demand, country-level revenue, and customer behavior.

## Business Questions

- What are the gross and net sales?
- How much revenue is reduced by cancellations and returns?
- Which months and countries generate the most revenue?
- Which products generate the highest net sales?
- Who are the most valuable customers, by total spend and by average order value?

## Dataset

## Dataset

**UCI Online Retail Dataset**
Source: [Kaggle / UCI ML Repository](https://www.kaggle.com/datasets/jihyeseo/online-retail-data-set-from-uci-ml-repo/data)
Records: 541,909 · Period: December 2010 – December 2011

Transactional invoice-line data from a UK-based online retailer. Each row is a single product line within an invoice — one invoice can span multiple rows. Columns include invoice number, product code/description, quantity, invoice date, unit price, customer ID, and country.

> The raw dataset is not included in this repo due to size (~44MB). Download it directly from the source link above if you want to reproduce the analysis.

## Tools

Python, Pandas, Matplotlib, Jupyter Notebook

## Approach

1. **Initial inspection** — structure, dtypes, missing values
2. **Data quality assessment**
   - Missing values: `Description` (0.27%), `CustomerID` (24.93%)
   - Exact duplicates: 5,268 rows (10,147 rows total involved)
   - Numerical anomalies: negative quantities (cancellations/returns vs. inventory adjustments), negative/zero unit prices
3. **Cleaning** — removed exact duplicates; kept missing-CustomerID rows for overall/product/country analysis but excluded them from customer-level analysis; investigated (rather than blindly dropped) missing descriptions
4. **Gross vs. Net sales datasets** — built separately, since each requires different filtering logic (gross = positive-only transactions; net = retains cancellations to reflect real revenue impact)
5. **Analysis** — monthly trend, country breakdown, product performance, customer value (total spend vs. average order value)
6. **Visualization** — line and horizontal bar charts for each of the above
7. **Export** — key result tables saved as CSV for reuse

## Key Findings

- Gross sales: ~10.64M · Net sales: ~9.75M · Cancellations/returns reduced revenue by ~8.4% (~894K)
- November 2011 was the strongest complete month (~1.46M net sales); December is incomplete in the dataset (ends Dec 9) and isn't a true decline
- The UK generated ~84% of net sales; the Netherlands was the top non-UK market
- `REGENCY CAKESTAND 3 TIER` was the top physical product by net sales
- One "top-selling" product (80,995 units in a single transaction) turned out to be fully cancelled 12 minutes later under a linked invoice — a reminder that gross figures alone can be misleading
- The customer with the highest total net sales was not the customer with the highest average order value — these measure different things

## What This Project Reinforced

Most of the effort here went into the data-quality layer, not the charts — deciding what to keep, what to exclude, and why, before trusting any aggregate number. That same discipline (systematic quality checks before transformation) carries directly into building ETL/ELT pipelines.

## Next Steps

Currently building full ETL/ELT pipelines using PostgreSQL, dbt, and Airflow as part of my transition toward Data Engineering.