# KPMG Data Analytics Consulting — Customer & Sales Analysis

An end-to-end Excel-based data analysis project built for KPMG's "Sprocket Central Pty Ltd" case study: a bike retailer that wants to identify its most valuable customers so it can target a marketing campaign at similar prospects. The workbook takes four raw, messy datasets through cleaning, segmentation, transaction analysis, and Customer Lifetime Value (CLV) modeling, and ends with an executive summary of findings and recommendations.

**Every single number in this workbook — cleaning and analysis alike — is a live Excel formula.** Nothing was pre-calculated in Python or another tool and pasted in as static values. Change a value in a `Raw_*` sheet and the results ripple all the way through to the executive summary.

## File

`KPMG_Data_Analysis_Project.xlsx`

## Datasets

Sourced from KPMG's public "Sprocket Central Pty Ltd" case study data:

| Raw sheet | Rows | Description |
|---|---|---|
| `Raw_Customer_Address` | ~4,000 | Customer addresses, postcode, state, country, property valuation |
| `Raw_Customer_Demographic` | ~4,000 | Customer names, gender, DOB, job title/industry, wealth segment, tenure, etc. |
| `Raw_Transactions` | ~20,000 | 2017 transaction-level sales data (product, price, cost, order status) |
| `Raw_New_Customer_List` | ~1,000 | Prospective customers to be scored/ranked for a marketing campaign |

The raw data intentionally includes real-world messiness — duplicate records, inconsistent categorical values (e.g. `"F"` vs `"Female"`, `"NSW"` vs `"New South Wales"`), missing fields, and even a few adversarial test strings (script tags, shell-injection-style text) — to mirror the kind of "dirty" data an analyst actually receives.

## Workbook Structure

| Sheet | Purpose |
|---|---|
| `Formula_Reference` | A guide documenting the exact Excel formula behind every cleaned column and every analytical metric in the workbook |
| `Raw_Customer_Address` / `Raw_Customer_Demographic` / `Raw_Transactions` / `Raw_New_Customer_List` | Untouched original data, exactly as supplied |
| `Customer_Address_Clean` / `Customer_Demographic_Clean` / `Transactions_Clean` / `New_Customer_List_Clean` | Cleaned versions of each raw dataset, computed via formulas (standardized categories, deduplication flags, validity flags) that reference the raw tabs |
| `Task2_Segmentation` | Customer segmentation by wealth segment and gender |
| `Task3_Transaction_Analysis` | Monthly sales trend, sales by brand and product line, top 10 customers by transaction value |
| `Task4_New_Customer_Insights` | Distribution of the 1,000 prospective customers by wealth segment, job industry, and state |
| `Task5_CLV_Analysis` | Customer Lifetime Value calculated per customer, and averaged by wealth segment / gender |
| `Task6_Executive_Summary` | Narrative summary of key findings plus marketing, expansion, and product recommendations |
| `Customer_Totals_Helper` | Hidden helper sheet aggregating each customer's total revenue and purchase count, feeding the CLV calculation |

## Methodology

### 1. Data Cleaning
Each `*_Clean` sheet is built entirely from formulas referencing its `Raw_*` counterpart:
- Standardizes inconsistent category labels (e.g. gender, state abbreviations)
- Flags duplicate `customer_id` records with `COUNTIF`-based logic
- Flags row validity for downstream filtering
- Derives helper fields (e.g. transaction month name/number) used in later analysis

See `Formula_Reference` for the exact formula behind every column.

### 2. Customer Segmentation
Customers are grouped by **wealth segment** (Mass Customer, Affluent Customer, High Net Worth) and by **gender**, with average tenure and average purchase behavior calculated per group.

### 3. Transaction Analysis
- Monthly sales trend across 2017
- Total sales by brand and by product line, with average list price
- Top 10 customers ranked by total transaction value

### 4. New Customer Insights
Cross-tabulates the 1,000 prospective customers by job industry and wealth segment, and profiles them by state, to identify where a marketing campaign should focus.

### 5. Customer Lifetime Value (CLV)
```
CLV = (Average Purchase Value × Purchase Frequency) × Customer Lifespan (Tenure)
```
Calculated per customer using the `Customer_Totals_Helper` sheet, then averaged by wealth segment and gender.

### 6. Executive Summary
Synthesizes all four analyses into key findings and three sets of recommendations: marketing strategy for high-value segments, business expansion by geography, and product offering improvements.

## Key Findings

- **Segmentation:** The 4,000-customer base splits into Mass Customer (50%), High Net Worth (26%), and Affluent Customer (24%), with near-identical average tenure (~10.5–10.7 years) across all three — tenure does not differentiate wealth segment.
- **Transactions:** Approved 2017 transactions generated **$21.74M** in total sales across 19,625 orders. Sales were stable month-to-month with no strong seasonality. The **Standard** product line drove ~71% of revenue ($15.49M) despite Touring and Road carrying higher average list prices — volume, not price, is the current revenue lever.
- **New customers:** The 1,000 prospects are concentrated in NSW (506), skew toward the Mass Customer segment (508), and represent an estimated **$48.7M** in potential revenue if converted at rates similar to existing customers (a directional estimate, not a forecast).
- **CLV:** Average CLV is remarkably flat across wealth segments (Mass $64,864 / High Net Worth $64,306 / Affluent $64,410, all within ~1% of each other) — a counter-intuitive result showing that **tenure and purchase frequency**, not the wealth-segment label, are the real drivers of long-run customer value.

## Recommendations (summary)

1. **Marketing:** Target by tenure and purchase frequency rather than wealth segment; use the Top-10 customer list as a seed for a VIP/loyalty program and look-alike prospecting.
2. **Expansion:** Prioritize NSW, followed by VIC and QLD, for acquisition campaigns, focusing on Mass Customer and Financial Services/Manufacturing prospects.
3. **Product:** Test price optimization/bundling on the high-volume Standard line; evaluate whether Road and Touring are under-marketed premium lines or a genuine niche; review the underperforming Mountain line.

Full detail is available in the `Task6_Executive_Summary` sheet of the workbook.

## How to Use This Workbook

1. Open `KPMG_Data_Analysis_Project.xlsx` in Excel (or a compatible spreadsheet tool that supports standard formulas — Excel is recommended for full formula fidelity).
2. Start with `Formula_Reference` to understand how each metric is derived.
3. Explore `Raw_*` → `*_Clean` → `Task2`–`Task5` in order to follow the data pipeline from raw input to analysis.
4. Read `Task6_Executive_Summary` for the narrative takeaways.
5. Because every cell is a live formula, you can edit any value in a `Raw_*` sheet and watch the downstream analysis and summary recalculate automatically.

## Tools & Skills Demonstrated

- Data cleaning and validation using native Excel formulas (`COUNTIF`, conditional logic, lookups)
- Pivot-style aggregation and cross-tabulation built with formulas
- Customer segmentation and cohort analysis
- Customer Lifetime Value (CLV) modeling
- Executive-level synthesis and business recommendation writing

---
*Based on the KPMG Data Analytics Consulting Virtual Internship case study (Sprocket Central Pty Ltd).*
