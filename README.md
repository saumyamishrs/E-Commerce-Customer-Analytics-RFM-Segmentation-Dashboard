
# Online Retail Customer Analytics & RFM Segmentation

An end-to-end data analytics project using SQL Server, Python (Pandas), and Power BI to analyze customer purchasing behavior, identify valuable customer segments, and understand customer churn risk.

> **Author:** Saumya Mishra

## Table of Contents

1. [Business Problem](#business-problem)
2. [Objectives](#objectives)
3. [Dataset](#dataset)
4. [Tech Stack](#tech-stack)
5. [Methodology](#methodology)
6. [Customer Segments](#customer-segments)
7. [Dashboard Overview](#dashboard-overview)
8. [Key Findings](#key-findings)
9. [Project Deliverables](#project-deliverables)
10. [Limitations](#limitations)
11. [Project Structure](#project-structure)
12. [How to Run](#how-to-run)
13. [Future Work](#future-work)
14. [Acknowledgements](#acknowledgements)

---

## Business Problem

Businesses need to understand which customers contribute the most revenue, which customers may be at risk of disengaging, and how purchasing behavior varies over time and across countries.

This project uses historical retail transaction data and Recency, Frequency, and Monetary (RFM) analysis to identify customer segments and generate insights that can support customer retention and marketing decisions.

## Objectives

- Identify high-value customers and customer segments.
- Analyze revenue contribution across customer segments.
- Identify inactive customers using a defined churn threshold.
- Explore revenue trends over time.
- Compare customer value and churn patterns across countries.
- Develop an interactive Power BI dashboard for business reporting.
- Translate analytical findings into actionable business recommendations.

## Dataset

- **Source:** [UCI Machine Learning Repository — Online Retail II](https://archive.ics.uci.edu/dataset/502/online%2Bretail%2Bii)
- **Records:** 1,067,371 transactions.
- **Period:** December 2009 – December 2011.
- **Key fields:** Invoice, product description, quantity, unit price, customer ID, and country.

The dataset contains historical transactions from a UK-based online retailer.

The raw dataset is not included in this repository. Download it from the official UCI source linked above.

## Tech Stack

| Layer | Tools |
|---|---|
| Data cleaning and preparation | SQL Server |
| Customer analysis and RFM segmentation | Python, Pandas |
| Interactive visualization | Power BI Desktop |
| Business documentation | Microsoft Word |
| Version control | Git, GitHub |

## Methodology

### 1. Data Cleaning

Used SQL to prepare transaction data for analysis by addressing duplicate and invalid records and preparing the data for subsequent analysis.

### 2. Exploratory Data Analysis

Examined transaction and customer data to understand purchasing behavior, revenue distribution, and customer activity.

### 3. RFM Analysis

Calculated customer-level RFM metrics:

- **Recency:** Time elapsed since the customer's most recent purchase.
- **Frequency:** Number of distinct purchase transactions.
- **Monetary:** Total customer spending during the analysis period.

These metrics provide a structured way to assess customer engagement and value.

### 4. Customer Segmentation

Applied RFM scoring to categorize customers according to their purchasing behavior and value. The resulting segments help distinguish high-value, loyal, inactive, and other customer groups.

### 5. Churn Analysis

Defined a customer as churned if they had no purchase during the trailing 90-day period, measured relative to the end of the historical dataset.

This is a rule-based churn definition, not a predictive machine learning model.

### 6. Dashboard Development

Developed an interactive Power BI dashboard to explore customer value, revenue contribution, segment performance, geographical patterns, and churn trends.

## Customer Segments

| Segment | Description |
|---|---|
| Champions | Customers with strong RFM profiles and high overall value. |
| Loyal | Customers with consistent purchasing behavior. |
| At Risk | Previously valuable customers whose purchase recency has declined. |
| New | Recent customers who have not yet established repeat purchasing behavior. |
| Needs Attention | Customers who may benefit from further engagement. |
| Lost | Customers with prolonged inactivity. |

*Note: Segment definitions depend on the RFM scoring rules implemented in the notebook.*

## Dashboard Overview

The Power BI report contains three pages.

### 1. Home / Navigation

Provides the dashboard entry point and navigation to the analysis pages.

### 2. Business Overview

Highlights key performance indicators and revenue patterns, including:

- Total customers
- Total revenue
- Churned customer percentage
- Average customer value
- Revenue by customer segment
- Revenue share by segment
- Revenue trends by month, quarter, and year

### 3. RFM Analysis

Supports deeper analysis of customer and country performance, including:

- Customer counts and revenue by country
- Average RFM scores
- Top countries by average customer value
- Churn percentage over time
- Customer segment comparisons
- Country-level customer analysis

Interactive filters support exploration by relevant time periods, country, and customer segment.

## Key Findings

The following figures are based on the project dashboard with no filters applied.

- **Customer base:** 5,881 customers.
- **Total revenue:** Approximately $17 million.
- **Average customer value:** Approximately $2,954.
- **Revenue concentration:** The Champions segment contributes approximately $11.8 million, or 68% of total revenue.
- **Churn:** 50.9% of customers are flagged as churned under the defined 90-day inactivity rule.
- **Seasonality:** November is the highest-revenue month, at approximately $2.32 million. Q4 is the strongest quarter, at approximately $6.2 million.
- **Yearly revenue:** Approximately $0.7 million in 2009, $8.4 million in 2010, and $8.3 million in 2011.
- **Geographical performance:** EIRE has the highest average customer value, at approximately $123,000.

### Business Interpretation

- The high revenue contribution from Champions highlights the importance of retaining valuable customers.
- Customers with declining purchasing activity may benefit from targeted retention campaigns.
- Seasonal revenue patterns can help businesses plan inventory and promotional activities.
- Country-level averages should be interpreted carefully because a small number of high-value buyers may influence the results.

*These findings should be interpreted in the context of the dataset, implemented calculations, and dashboard filters.*

## Project Deliverables

The repository contains the following project artifacts:

- **SQL script:** Data-cleaning and preparation queries.
- **Python notebook:** Customer analysis and RFM segmentation.
- **Power BI dashboard:** Interactive customer and business analytics.
- **Business Requirements Document:** Project requirements and business scope.
- **README:** Project documentation, methodology, and key findings.

## Limitations

- The churn threshold is fixed at 90 days and is not statistically derived.
- The dataset covers historical transactions ending in December 2011. Churn is measured relative to the historical dataset's end date, not the present day.
- Wholesale and retail customers are not explicitly separated, which may affect customer-value comparisons.
- Country-level averages can be influenced by a small number of high-value customers.
- The project does not include predictive churn modelling or real-time customer scoring.
- Results depend on the data-cleaning rules, RFM scoring logic, and assumptions implemented in the project files.

## Project Structure

```text
online-retail-customer-analytics-rfm/
├── BRD.docx
├── Online_retail_dashboard.pbix
├── RFM SEGMENTATIOM.ipynb
├── online_retail_data_cleaning.sql
└── README.md
```

## How to Run

### Prerequisites

- Microsoft SQL Server and SQL Server Management Studio (SSMS)
- Python and Jupyter Notebook
- Required Python libraries used in the notebook, including Pandas
- Power BI Desktop

### Steps

1. Download the Online Retail II dataset from the [official UCI repository](https://archive.ics.uci.edu/dataset/502/online%2Bretail%2Bii).
2. Open `online_retail_data_cleaning.sql` in SQL Server Management Studio.
3. Review the SQL script and configure the database, table names, and data-source paths as required.
4. Open `RFM SEGMENTATIOM.ipynb` in Jupyter Notebook or another compatible notebook environment.
5. Install any missing Python dependencies and execute the notebook cells in order.
6. Open `Online_retail_dashboard.pbix` in Power BI Desktop.
7. If prompted, configure the data-source paths and refresh the data.
8. Refer to `BRD.docx` for the business requirements and project scope.

**Note:** The SQL script, notebook, and Power BI report may require local configuration before they run successfully.

## Future Work

- Evaluate alternative churn thresholds and compare their effects on customer classification.
- Explore predictive churn modelling using appropriate historical customer features.
- Analyze wholesale and retail customers separately where possible.
- Add product-level analysis and customer-specific recommendations.
- Explore automated refresh and recurring customer-segmentation workflows.
- Add dashboard screenshots to the README for a quicker visual overview.

## Acknowledgements

- **Dataset:** [Online Retail II — UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/502/online%2Bretail%2Bii), donated by Daqing Chen.
- **Tutorial inspiration:** Customer Analytics & RFM Segmentation tutorial by Mansi Goel.

---

*This project demonstrates the application of SQL, Python, customer segmentation, and Power BI to practical business analytics questions.*


