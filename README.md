# superstore-sales-sql-analysis
SQL-based exploratory analysis of the Superstore sales dataset using BigQuery. Includes revenue breakdown by category, region, and year, along with business-driven insights. Demonstrates aggregation, filtering, grouping, and real-world analytical thinking for data analytics and engineering workflows.

Retail Revenue Analysis (SQL + Excel)
This project analyses a retail sales dataset using SQL (BigQuery) and Excel to identify revenue drivers, product performance, and year-over-year trends. 
The aim was to simulate a real-world data analyst workflow:
Query raw transactional data
Aggregate and segment performance
Identify trends and anomalies
Translate findings into business recommendations

Tools Used
Google BigQuery (SQL)
Microsoft Excel
GitHub (project documentation)

Dataset
Retail transactional dataset (~9,800 rows)
U.S. regional sales data

Product hierarchy:
Category
Sub-Category
Sales metrics over multiple years

Analytical Workflow
1) Understanding the Dataset

Initial exploration focused on:
Row count
Geographic scope
Product structure
Time coverage

Key findings
Each row represents a product-level sale
Dataset operates only within the United States
Data spans multiple years of transactions

<img width="2048" height="1280" alt="image" src="https://github.com/user-attachments/assets/68810cfd-3032-4ba8-82cf-7c9580986109" />
<img width="2048" height="1280" alt="image" src="https://github.com/user-attachments/assets/752112e0-f726-4ef2-b72b-8484d1a5fae9" />

Row count query

DISTINCT region output

2) Total Revenue Calculation
SELECT
  SUM(Sales) AS total_revenue
FROM `project-ad0cc66f-e8dd-4dcf-852.superstore_sales.project01`;

Result: ~2.26M total revenue

Insight
Dataset represents a multi-million revenue business
Suitable for meaningful performance and trend analysis

<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/23a7155c-ba3d-484d-b601-2da5b20fe0f2" />
<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/775c8c12-e88f-4ead-aaed-20eabace0ae1" />

3) Revenue by Region
SELECT
  Region,
  SUM(Sales) AS total_revenue
FROM `project-ad0cc66f-e8dd-4dcf-852.superstore_sales.project01`
GROUP BY Region
ORDER BY total_revenue DESC;

Findings
East and West generate highest revenue
South underperforms comparatively

Business interpretation
Regional performance is uneven — potential opportunity for targeted marketing and operational optimisation.

<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/b9e7de38-ac93-4925-baa1-ce848320bd81" />
<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/664ff466-83b4-4560-bba7-66bc177e2234" />

4) Revenue by Category
SELECT
  Category,
  SUM(Sales) AS total_revenue
FROM `project-ad0cc66f-e8dd-4dcf-852.superstore_sales.project01`
GROUP BY Category
ORDER BY total_revenue DESC;

Findings
Technology is the dominant revenue driver
Furniture second
Office Supplies third

Insight
Technology is the core revenue engine across the business.

<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/bc2bf075-b2a7-478d-ab46-42991342393e" />
<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/b605ee28-eb3a-4885-a9d9-c3354cad08fe" />

5) Revenue by Sub-Category
SELECT
  `Sub-Category`,
  SUM(Sales) AS total_revenue
FROM `project-ad0cc66f-e8dd-4dcf-852.superstore_sales.project01`
GROUP BY `Sub-Category`
ORDER BY total_revenue DESC;

Findings
Phones and Chairs are strong contributors
Envelopes, Labels, and Fasteners underperform

Learning moment
Early challenges included referencing column names containing hyphens (Sub-Category).
This required using backticks rather than single quotes:
'Sub-Category' → treated as a string
`Sub-Category` → correct column reference
This reinforced understanding of SQL syntax and debugging workflow.

<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/d67db82f-9c51-4384-b037-7b19d7fc4657" />
<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/dca09f35-01ef-49ad-a794-6c1466eb5bd6" />

6) Segmenting Performance with HAVING
Sub-categories were grouped into performance tiers:
High: > 100,000 revenue
Medium: 20,000–100,000
Low: < 20,000
This introduced filtering aggregated results using HAVING.

Key learning
WHERE filters rows before aggregation
HAVING filters results after aggregation
A major conceptual shift in understanding SQL execution order.

<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/c2b03d00-70e5-4e4d-b2ac-b3150fbfca54" />
<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/53ca666f-3deb-4551-9396-688f2f387180" />
<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/7c769522-11cf-4513-b2e3-c36c0bf551d4" />
<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/c08eddcb-d7e9-4828-8e9a-d414b6de9585" />
<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/fb0a11f1-2f15-4cd9-a7d6-8cacd96bd060" />
<img width="2048" height="1188" alt="image" src="https://github.com/user-attachments/assets/c413a450-700f-489b-bd82-9d09d806d33d" />

7) Year-over-Year Revenue Trends
SELECT
  EXTRACT(YEAR FROM Order_Date) AS year,
  SUM(Sales) AS total_revenue
FROM `project-ad0cc66f-e8dd-4dcf-852.superstore_sales.project01`
GROUP BY year
ORDER BY year;

Findings
Overall upward trend
Revenue dip in 2016
Strong growth in 2017 and 2018
2018 strongest year

Interpretation
Growth is non-linear, suggesting operational or market changes rather than steady organic expansion.

<img width="3104" height="1802" alt="image" src="https://github.com/user-attachments/assets/04d5122b-f01a-4151-8024-56fddfdf5b68" />
<img width="3104" height="1802" alt="image" src="https://github.com/user-attachments/assets/b27697b5-f78e-476a-941f-9cad86d42a97" />


8) Category Trends Over Time (Excel Analysis)
Revenue by year and category was exported into Excel for readability and comparison.

<img width="2048" height="1190" alt="image" src="https://github.com/user-attachments/assets/72b1ff3b-e259-4bb6-8cf2-40ab2a801bd6" />

Observations
Technology shows strongest long-term growth
Furniture briefly outperformed Technology in 2016
Office Supplies dipped before recovering

Business insight
Revenue growth alone does not indicate business health — cost and margin analysis is required.

Key Business Recommendations
Prioritise investment in Technology category (inventory, marketing, expansion)
Investigate Furniture’s 2016 spike for one-off drivers
Analyse underperforming sub-categories for optimisation
Conduct profitability modelling before scaling operations

What I Learned
Applying SQL aggregation (SUM, GROUP BY, HAVING)
Understanding SQL execution order
Debugging column reference issues
Translating data into stakeholder-focused insights
Structuring analysis for portfolio presentation

Next Steps
Incorporate cost data for profit analysis
Build automated reporting tables
Develop dashboard layer (Power BI / Looker)
Expand into data engineering workflows (data modelling, pipelines)

Project Purpose
This project demonstrates practical SQL analysis skills, business thinking, and the ability to communicate insights — key competencies for data analyst and early data engineering roles.
