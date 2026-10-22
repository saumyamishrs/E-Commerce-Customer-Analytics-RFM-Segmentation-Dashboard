# Online Retail Customer Analytics & RFM Segmentation

An end-to-end customer analytics project that identifies the most valuable customer segments and quantifies churn risk for a UK-based, non-store online retailer of gift ware and home decor. Results are delivered through an interactive **Power BI dashboard**.


## Table of Contents

1. [Business Problem](#business-problem)
2. [Objectives & Business Questions](#objectives--business-questions)
3. [Dataset](#dataset)
4. [Tech Stack](#tech-stack)
5. [Methodology](#methodology)
6. [Customer Segments](#customer-segments)
7. [Dashboard Overview](#dashboard-overview)
8. [Key Findings](#key-findings)
9. [Deliverables](#deliverables)
10. [Scope, Assumptions & Limitations](#scope-assumptions--limitations)
11. [Project Structure](#project-structure)
12. [How to Run](#how-to-run)
13. [Future Work](#future-work)
14. [Acknowledgements](#acknowledgements)

---

## Business Problem

Leadership has no structured, data-driven view of which customers drive the most revenue or which are showing early signs of disengagement. Retention and marketing efforts have been **reactive rather than targeted**, and spend is not prioritised toward the customers most likely to respond. A meaningful share of customers are wholesale buyers, which adds complexity to how customer value should be interpreted.

## Objectives & Business Questions

Identify the most valuable customer segments and quantify churn risk so that Marketing, CRM and Retention teams can focus effort and spend where it matters most.

The analysis answers:

- Who are our most valuable customers, and how much revenue do they contribute?
- Which customers have gone quiet and are at risk of churning?
- How do customer value and retention trend over time (month-over-month, year-over-year)?
- How do customer value and churn risk differ across countries?
- What concrete actions should the business take for each segment?

## Dataset

- **Source:** [Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii), UCI Machine Learning Repository (donated by Daqing Chen)
- **Size:** 1,067,371 transaction rows
- **Period:** December 2009 – December 2011
- **Fields:** invoice, product description, quantity, unit price, customer ID, country
- A backup copy of the raw data is maintained in this repository in case the source becomes unavailable.

## Tech Stack

| Layer | Tool |
| --- | --- |
| Data extraction & cleaning | SQL |
| RFM scoring & segmentation | Python |
| Visualisation & reporting | Power BI Desktop |
| GitHub |

## Methodology

1. **Extract & clean (SQL)** – remove duplicates and invalid records to produce an analysis-ready transaction dataset.
2. **Compute RFM metrics (Python)** – per customer:
   - **Recency:** days since the most recent purchase
   - **Frequency:** number of distinct purchase transactions
   - **Monetary:** total revenue in the analysis period
3. **Score & segment** – convert R, F and M into scores and assign each customer to a segment.
4. **Flag churn** – a customer is **churned** if they have **no purchase in the trailing 90 days**.
5. **Visualise (Power BI)** – load customer-level outputs into a multi-page interactive dashboard with slicers for Month, Quarter, Year, Country, Segment and IsChurned.

## Customer Segments

| Segment | Description |
| --- | --- |
| **Champions** | High recency, frequency and monetary value – the most valuable customers |
| **Loyal** | Consistent purchase history with moderate-to-high value |
| **At Risk** | Previously valuable customers whose recency has recently dropped |
| **New** | Recent first-time customers not yet established as repeat buyers |
| **Needs Attention** | Moderate recency but low purchase frequency |
| **Lost** | No meaningful activity for an extended period |

## Dashboard Overview

The Power BI report has three pages:

1. **Home / Navigation** – entry point linking to the other pages.
2. **Business Overview** – KPIs (Total Customers, Total Revenue, Churned %, Avg Customer Value), revenue by segment, revenue share by segment, and revenue by month, quarter and year.
3. **RFM Analysis** – country performance summary (customers, revenue, average R/F/M scores), top 5 countries by average customer value, and churn % by month, quarter and year. Toggle between **Segment** and **Country** views.

<!-- Add screenshots, e.g.: ![Business Overview](images/business_overview.png) -->

## Key Findings

Figures are from the dashboard with no filters applied.

- **Scale:** 5,881 customers generating about **$17M** in revenue; average customer value is about **$2,954**.
- **Revenue concentration:** **Champions contribute roughly $11.8M (~68%)** of total revenue.
- **Churn:** **50.9%** of customers are flagged as churned under the 90-day rule.
- **Seasonality:** revenue builds through the second half of the year, peaking in **November (~$2.32M)**; **Q4 is the strongest quarter (~$6.2M)**.
- **Yearly trend:** about $0.7M in 2009 (partial year, data starts in December), about $8.4M in 2010 and about $8.3M in 2011.
- **Churn trend:** churn % was 40.2% in 2009, 56.3% in 2010 and 31.5% in 2011, and it declines across the quarters of the year.
- **Geography:** average customer value is highest in **EIRE (~$123K)**, followed by Singapore, Netherlands, Australia and Denmark. A few high-value (likely wholesale) buyers may drive these figures, so interpret with care.

## Deliverables

- Cleaned, deduplicated, analysis-ready transaction dataset
- Customer-level RFM scores and segment assignments
- Churn-flagged customer list (90-day threshold)
- Three-page Power BI dashboard (`.pbix`) and PDF export
- Written summary of key findings and recommended actions per segment
- Business Requirements Document (BRD)

## Scope, Assumptions & Limitations

**In scope:** SQL data cleaning, RFM segmentation in Python, fixed-threshold churn flag, interactive Power BI dashboard.

**Out of scope:** predictive churn modelling, product-level recommendations, real-time or automated customer scoring, execution of marketing campaigns.

**Assumptions & limitations:**

- Churn uses a fixed **90-day inactivity threshold** (chosen for simplicity and interpretability, not statistically derived).
- Wholesale and retail customers are **not separated** unless the data clearly distinguishes them, which can skew value metrics.
- The analysis uses **historical transaction data only** and does not account for promotions or other external drivers of seasonality.
- Since the data ends in December 2011, "trailing 90 days" is measured relative to the end of the dataset, not today's date.

## Project Structure

> Suggested layout – adjust to match your repository.

```
├── data/
│   ├── raw/                 # Original Online Retail II backup
│   └── processed/           # Cleaned data, RFM scores, churn list
├── sql/                     # Extraction & cleaning queries
├── notebooks/               # Python RFM segmentation
├── dashboard/
│   ├── Dashboard.pbix       # Power BI report
│   └── Dashboard.pdf        # Exported report
├── docs/
│   └── BRD.docx
└── README.md
```
## Dataset
- Source: [UCI Machine Learning Repository — Online Retail II](https://archive.ics.uci.edu/dataset/502/online%2Bretail%2Bii)
- The dataset contains approximately 1.07 million retail transactions.
- The raw dataset is not included in this repository; download it from the official UCI source.

## How to Run
1. **Clone** the repository and place the raw dataset in `data/raw/`.
2. **Run the SQL scripts** in `sql/` to clean and deduplicate the data.
3. **Run the Python notebook** in `notebooks/` to compute RFM scores, segments and the churn flag, then export the customer-level output.
4. **Open the `.pbix`** file in Power BI Desktop, point the data source to your processed files, refresh, and explore with the slicers.

## Future Work

- Move from a fixed 90-day rule to a **predictive churn model**.
- Separate **wholesale vs. retail** customers for cleaner value analysis.
- Add **product-level** insights and recommendations.
- Automate **customer scoring** on a recurring schedule.

## Acknowledgements

This project was built by following and adapting the [Customer Analytics & RFM Segmentation tutorial] by Mansi Goel. The dataset is Online Retail II from the UCI Machine Learning Repository (donated by Daqing Chen).
