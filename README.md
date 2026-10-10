# Retail E-commerce Sales & Customer Analytics (Power BI)

End-to-end Power BI project on 1M+ real transactions from the UCI Online Retail II dataset (UK online retailer, Dec 2009 - Dec 2011).

## Report Pages

### 1. Executive Overview
![Executive Overview](RetailEcommerce%20default%20state%20screenshots/1_executive_overview.png.png)

### 2. Product & Category Analysis
![Product & Category](RetailEcommerce%20default%20state%20screenshots/2_product_category.png.png)

### 3. Customer & RFM Analysis
![Customer & RFM](RetailEcommerce%20default%20state%20screenshots/3_customer_Rfm.png.png)

### 4. Returns & Cancellations
![Returns & Cancellations](RetailEcommerce%20default%20state%20screenshots/4_Returns%20%26%20cancellation.png.png)

## Data Model
Star schema: 2 fact tables (Fact_sales, Fact_returns) and 3 dimensions (Dim_Customer, Dim_Product, Dim_Date), all one-to-many with single-direction filtering.

## Key Work
- **Power Query:** removed non-sale bookkeeping rows, split cancellations into a separate fact table, built a keyword-based product Category column
- **DAX:** Revenue, Net Revenue, Cancellation Rate, Average Order Value, YTD / Prior Year / YoY, Revenue Target
- **RFM segmentation:** Recency, Frequency, Monetary, quintile scoring with RANKX, and segment labels (Champions, Loyal, At Risk, Lost, etc.)
- **Dynamic RLS:** LOOKUPVALUE + USERPRINCIPALNAME() against a user-access mapping table

## Data Issues Found and Resolved
- Power Query is case-sensitive but the data model is not, which caused a false many-to-many relationship (fixed by standardizing StockCode casing)
- Date vs DateTime mismatch between the date table and the fact tables, which broke date filtering
- Null Customer IDs and unmatched StockCodes causing blank buckets in visuals

## Known Limitations
- A small number of customers have a different Country in Dim_Customer than in their transactions
- Category is derived from keyword matching, so a large share of products fall in "Other"
- Scatter chart axis capped to keep the main cluster readable

## Files
- `RetialEcommerce_project.pbix` Power BI report
- `RetialEcommerce_project_pdf.pdf` full report export
- `RetailEcommerce default state screenshots/` page previews
