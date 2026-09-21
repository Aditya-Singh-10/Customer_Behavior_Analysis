# 🛍️ Customer Shopping Behavior Analysis

An end-to-end data analytics project that takes raw customer shopping data through **Python cleaning → PostgreSQL analysis → DAX measures → Power BI dashboard** to uncover buying patterns, customer segments, and actionable business recommendations.

---

## 📌 Project Overview

| Item | Details |
|---|---|
| **Dataset size** | 3,900 rows × 18 columns |
| **Data cleaning & feature engineering** | Python (pandas) in Jupyter Notebook |
| **Database & analysis** | PostgreSQL (loaded via SQLAlchemy), 10 business-question queries |
| **Modelling & visualisation** | DAX + Power BI |
| **Goal** | Understand who the customers are, what they buy, and what drives revenue and loyalty |

---

## 🎯 Business Objectives

- Identify which customer segments (age, gender, location, subscription status) drive the most revenue
- Understand product and category performance
- Analyse the impact of discounts, shipping type, and payment method on purchasing behaviour
- Measure customer loyalty and repeat-purchase patterns
- Provide data-backed recommendations to improve sales and retention



---

## 🛠️ Tech Stack

- **Python** — pandas, NumPy, SQLAlchemy, Jupyter Notebook
- **PostgreSQL** — data storage and SQL analysis
- **Power BI** — data modelling, DAX, interactive dashboard
- **Gamma** — project presentation deck

---

## 🔄 Project Workflow

```
Raw CSV → Jupyter (clean + feature engineering) → PostgreSQL (SQLAlchemy load)
        → SQL analysis (10 queries) → Power BI (DAX + dashboard) → Insights & recommendations
```

---

## 1️⃣ Data Cleaning & Feature Engineering (Jupyter Notebook)

**Notebook:** `Customer_Shopping_Behavior_Analysis.ipynb`

**Steps performed:**

1. **Data loading** — imported the raw CSV into a pandas DataFrame
2. **Initial exploration** — `.head()`, `.info()`, `.describe()`, shape and data types check
3. **Missing values** — identified null values per column and handled them (e.g., imputation / removal — *describe what you did*)
4. **Duplicates & consistency** — checked for duplicate records and standardised column names (snake_case)
5. **Feature engineering** — created new columns to support analysis, for example:
   - Age groups (e.g., Young Adult, Adult, Middle-aged, Senior)
   - Purchase frequency in days / numeric conversions
   - *Add any other columns you created*
6. **Load to PostgreSQL** — connected using SQLAlchemy and wrote the cleaned DataFrame to a PostgreSQL table

```python
from sqlalchemy import create_engine

engine = create_engine("postgresql+psycopg2://<user>:<password>@localhost:5432/<database>")
df.to_sql("customer", engine, if_exists="replace", index=False)
```

> ⚠️ Never commit real credentials. Use environment variables or a `.env` file.

---

## 2️⃣ Exploratory Data Analysis in PostgreSQL

**File:** `SQL.sql`

Ten business-driven queries were written to answer key questions. Replace the descriptions below with your exact questions:

| # | Business Question | SQL Concepts Used |
|---|---|---|
| 1 | Revenue by gender | `SUM`, `GROUP BY` |
| 2 | Discount-using customers who still spent above average | Subquery / `AVG` |
| 3 | Top 5 highest-rated products | `AVG`, `ORDER BY`, `LIMIT` |
| 4 | Standard vs Express shipping — average purchase amount | `CASE`, `GROUP BY` |
| 5 | Subscribers vs non-subscribers — spend & revenue | `GROUP BY`, aggregates |
| 6 | Products with highest discount-based purchase percentage | Conditional aggregation |
| 7 | Customer segmentation (New / Returning / Loyal) | `CASE`, CTE |
| 8 | Top 3 products per category | Window functions (`ROW_NUMBER`) |
| 9 | Repeat buyers and subscription likelihood | `CASE`, aggregation |
| 10 | Revenue by age group | `GROUP BY`, derived column |

> These are placeholders — edit each row so it matches your real `SQL.sql`.

**Sample query:**

```sql
SELECT gender, SUM(purchase_amount) AS total_revenue
FROM customer
GROUP BY gender;
```

---

## 3️⃣ DAX Measures (Power BI)

The cleaned data was imported into Power BI, and DAX measures were created for the KPI cards and visuals. Update these to match the measures in your `.pbit` file:

```DAX
Total Customers = DISTINCTCOUNT(customer[customer_id])

Total Revenue = SUM(customer[purchase_amount])

Average Purchase Amount = AVERAGE(customer[purchase_amount])

Average Review Rating = AVERAGE(customer[review_rating])

Subscriber % =
DIVIDE(
    CALCULATE(COUNTROWS(customer), customer[subscription_status] = "Yes"),
    COUNTROWS(customer)
)

Discount Usage % =
DIVIDE(
    CALCULATE(COUNTROWS(customer), customer[discount_applied] = "Yes"),
    COUNTROWS(customer)
)
```

---

## 4️⃣ Power BI Dashboard

**File:** `Customer_Behavior_Dashboard.pbit`

**Dashboard highlights:**

- **KPI cards** — Total Customers, Total Revenue, Average Purchase Amount, Average Review Rating
- **Revenue by category / product**
- **Customer segmentation** — by age group, gender, and subscription status
- **Discount & shipping analysis**
- **Interactive slicers** — filter by category, gender, age group, subscription status, etc.

📸 *Add dashboard screenshots here:*

```markdown
![Dashboard Overview](images/dashboard_overview.png)
```

---

## 💡 Key Insights & Recommendations

*Fill in from your report — a few examples of the format:*

- **Insight:** [e.g., Subscribers contribute X% of revenue]
  **Recommendation:** [e.g., Promote subscription with targeted offers]
- **Insight:** [e.g., Discounts drive purchases in specific products]
  **Recommendation:** [e.g., Limit discounts to products that need a boost]
- **Insight:** [e.g., Loyal customers form the largest segment]
  **Recommendation:** [e.g., Launch a loyalty rewards program]

---

## ▶️ How to Run This Project

1. **Clone the repository**
```bash
   git clone https://github.com/<your-username>/customer-shopping-behavior-analysis.git
   cd customer-shopping-behavior-analysis
```
2. **Install dependencies**
```bash
   pip install pandas numpy sqlalchemy psycopg2-binary jupyter
```
3. **Run the notebook** — open `Customer_Shopping_Behavior_Analysis.ipynb` and run all cells
4. **Set up PostgreSQL** — create a database, update the connection string, and load the cleaned data
5. **Run SQL queries** — execute `SQL.sql` in pgAdmin / DBeaver / psql
6. **Open the dashboard** — open `Customer_Behavior_Dashboard.pbit` in Power BI Desktop and connect it to your data source

---

## 📈 Skills Demonstrated

`Data Cleaning` · `Feature Engineering` · `pandas` · `SQLAlchemy` · `PostgreSQL` · `CTEs & Window Functions` · `DAX` · `Data Modelling` · `Power BI Dashboarding` · `Business Storytelling`

---


---

⭐ If you found this project useful, consider giving it a star!
