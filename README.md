# Data Pipeline and Tool Mastery: Global Superstore

A small ETL (Extract, Transform, Load) pipeline built on the Global Superstore dataset (51,290 orders, 2011 to 2014). It uses three industry tools: Pandas, SQL (SQLite) and Matplotlib/Seaborn.

Built for **Yuva Intern, Data Engineer Internship, Task 4**.
Author: **Arifa Begum R**

## Tools Used

|          Tool          |                 Used for                          |
|------------------------|---------------------------------------------------|
| Python and Pandas      | Extracting and cleaning the data                  |
| SQL (SQLite)           | Storing the data and answering business questions |
| Matplotlib and Seaborn | Visualizing the results                           |

## Pipeline Overview

1. **Extract:** load the CSV (`latin-1` encoding), 51,290 rows and 24 columns, and inspect types, missing values and duplicates.
2. **Transform:** a reusable `clean_orders()` function that
   - drops `Postal Code` and `Row ID`
   - renames columns to lowercase with underscores
   - converts dates (day-month-year) to datetime
   - adds `order_year`, `order_month`, `delivery_days`, `is_loss` and `discount_band`
3. **Validate:** 7 data quality checks (no missing values, no duplicates, valid dates, discount between 0 and 1, positive quantity and sales, valid years). All pass.
4. **Load:** write the cleaned data to an SQLite table `orders` with indexes on `order_year`, `category` and `market`.
5. **Query:** six business questions in SQL using `GROUP BY`, window functions (`RANK`, `LAG`) and a CTE.
6. **Visualize:** four charts, including a market-by-category margin heatmap.
7. **Compare:** the same question answered in Pandas and SQL gives identical results.
8. **Automate:** `run_pipeline(csv_path)` runs extract, transform, validate and load in one call.

## Key Findings

- **Overall:** 12.64M sales, 1.47M profit, 11.6% margin; 24.5% of orders lose money.
- **Discounts are the biggest driver of losses.** Orders with no discount never lose money, while 98.4% of orders with a discount above 40% do. About 81% of all loss-making orders have a discount above 20%.
- **Tables** is the only sub-category that loses money (-64,083 profit, -8.5% margin) and is the main reason Furniture earns so little.
- **EMEA** has the lowest margin (5.4%) and is weak across all three categories, so the problem is market-wide.
- **US Furniture** is the weakest market and category pair (2.5% margin).
- **Growth:** sales rose 18.5% (2012), 27.2% (2013) and 26.3% (2014); 2014 sales were almost double 2011.

## Project Structure

```
data-pipeline-tool-mastery/
├── <notebook-name>.ipynb   # full pipeline, queries and charts
├── data/                   # Global Superstore CSV (not included if too large)
└── README.md
```

## How to Run

1. Clone the repository
```bash
   git clone https://github.com/arifabegum-2105/data-pipeline-tool-mastery.git
   cd data-pipeline-tool-mastery
```
2. Install the requirements
```bash
   pip install pandas numpy matplotlib seaborn jupyter
```
   (`sqlite3` ships with Python.)
3. Put the Global Superstore CSV in the project folder and set `path` in the notebook.
4. Open the notebook in Jupyter and run all cells.

## Next Steps

Apply the same pipeline to a new dataset and load it into a PostgreSQL database.
