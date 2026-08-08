# Superstore Sales - SQL Analysis

End-to-end SQL business performance analysis of a fictional US 
retail company - investigating regional profitability, product 
performance, discount impact, customer value, and revenue trends 
using SQLite and pandas.

## Business questions answered
1. Which regions generate the most revenue and profit - and why 
   do margins differ so significantly between them?
2. Which product sub-categories are loss-making, and what's driving it?
3. At what discount level does profit turn negative?
4. Who are the most and least profitable customers?
5. What is the monthly revenue trend and seasonal pattern?
6. Does shipping mode affect profitability?

## Key findings

### The central insight
A single theme connects almost every finding: **discount discipline 
is the primary driver of profitability** - not region, product 
category, ship mode, or customer segment.

### Finding 1 - Central region sacrifices margin for volume
Central generates strong revenue (USD 501k) but the lowest margin 
of any region (7.9%) - driven by a 24.0% average discount, more 
than double the West's 10.9%. The South generates USD 110k less 
revenue but a 4-point higher margin (11.9%).

### Finding 2 - Loss-making sub-categories are a pricing problem
Only three sub-categories are loss-making: Tables (USD -17,725), 
Bookcases (USD -3,473), and Supplies (USD -1,189). Tables and 
Bookcases generate USD 207k and USD 115k in revenue respectively - the losses are caused by aggressive discounting (26.1% and 
21.1%), not low demand.

### Finding 3 - Hard discount tipping point at 20%
Margins collapse from +29.5% (no discount) to -15.3% (21–40% 
discount) to -77.4% (40%+ discount). Nearly 14% of all orders 
are loss-making. The Very High tier generates USD 129k in revenue 
but destroys USD 100k in profit - the business would be more 
profitable not making these sales at all.

### Finding 4 - Loss-making customers span all segments
Cindy Stewart generates USD 5,690 in revenue but USD -6,626 in 
profit. Sean Miller generates USD 25,043 in revenue (highest in 
bottom 10) yet still USD -1,981 in profit. The problem is discount 
discipline at the individual account level, not customer segment.

### Finding 5 - Consistent seasonal growth pattern
Clear annual peaks in September and November/December across 
all four years. Revenue growing year-over-year - peak monthly 
revenue up ~44% from 2014 to 2017. Cumulative revenue reached 
USD 2.2M by December 2017.

### Finding 6 - Ship mode does not drive profitability
Margins range from 12.1% to 13.9% across all four ship modes - 
a negligible difference. Discount discipline matters far more 
than shipping optimisation.

## SQL concepts demonstrated
- Aggregations (SUM, AVG, COUNT, GROUP BY, ORDER BY)
- CASE statements - discount tier bucketing
- CTEs (Common Table Expressions) - customer profitability analysis
- Window functions - LAG, running totals, MoM growth calculation
- JULIANDAY - days-to-ship calculation
- Multi-level GROUP BY - category and sub-category analysis
- Subqueries and derived tables

## Why pd.read_sql over ipython-sql
Results are returned directly as pandas DataFrames - the same 
pattern used in production against PostgreSQL, Redshift, and 
Snowflake. Just swap the SQLAlchemy connection string for any 
database backend:
- SQLite (local): `create_engine('sqlite://')`
- PostgreSQL: `create_engine('postgresql://user:pass@host/db')`
- Snowflake: `create_engine('snowflake://user:pass@account/db')`
- Redshift: `create_engine('redshift+psycopg2://user:pass@host/db')`

## Tools used
Python · pandas · SQLite · SQLAlchemy · 
Matplotlib · Seaborn · Jupyter Notebook

## Dataset
Sample Superstore (Kaggle) - 9,994 orders · 2014–2017  
Columns: order date, ship date, customer, segment, region, 
category, sub-category, sales, quantity, discount, profit

## How to run
```
pip install pandas sqlalchemy jupyter matplotlib seaborn
jupyter notebook
```
Open `superstore_sql_analysis.ipynb` → Kernel → Restart & Run All
