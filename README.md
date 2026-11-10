# Churn-Analysis-Customer-Intelligence

OTT Subscription Platform | Python · SQL · pandas · seaborn
End-to-end churn analytics project for an OTT streaming service (think Netflix, Hotstar or Prime). It pulls multi-table subscriber data from a SQL database into Python, cleans it, engineers features, and calculates 20+ KPIs. The aim is to find who is churning, why, and when, and to turn those findings into retention actions.
Business Problem
In a crowded OTT market, keeping subscribers matters more than winning new ones. Acting as a Data Analyst, the goal is to identify high-risk subscribers using customer demographics, subscription tiers and support escalations, and to quantify the revenue at stake.
How churn is defined here: a membership that has been cancelled or become inactive.
The analysis answers three questions:
•	Who: which customers left, or are likely to leave
•	Why: how they behaved before leaving (plan, contract, complaints, escalations)
•	When: the "danger zone" where users drop off
Tech Stack
Area	Tools
Data extraction	sqlite3, pandas (SQL queries in Python)
Cleaning & feature engineering	pandas, numpy
Analysis (EDA)	pandas (group by, aggregation, pivot tables)
Visualisation	matplotlib, seaborn
Environment	Jupyter Notebook
Data Model
Database: customer_churn (three related tables joined on customerid)
Table	Key columns
db_customer	customerid, name, country, state, gender, dob, interests, pincode
db_subscription	customerid, subscription_start_date, subscription_type, renewal_date, plan_type, contract_type, cancellation_date, cancellation_reason, monthly_charges, cltv, churn_score
db_support	customerid, complaint_date, escalations, csat_score, comment
Workflow
1.	Connect & extract: connect Python to the SQLite database and pull the tables with SQL.
2.	Clean: fix data types, rename and select columns, run quality checks, handle missing values.
3.	Engineer features: calculate tenure and customer age, add churn flags and risk tiers.
4.	Analyse: aggregate churn by plan, contract, state and month.
5.	Visualise: chart the drivers with matplotlib and seaborn.
6.	Report: write up key insights, recommended actions and business impact.
KPIs Calculated
KPI	Formula
Churn rate	churned customers / total customers
Retention rate	1 − churn rate
Churn by plan / state	churn rate grouped by plan_type, country, state
ARPU	SUM(monthly_charges) / COUNT(active customers)
Average tenure	AVG(cancellation_date or today − subscription_start_date)
Revenue at risk	SUM(monthly_charges) where churn_score > 70
Escalation rate	SUM(escalations) / COUNT(complaints) × 100
Avg complaints per customer	COUNT(complaints) / COUNT(DISTINCT customerid)
Escalation → churn link	churn rate where escalations ≥ 1 vs 0
Key Findings
•	Churn rate: 28.6%, so retention is 71.4%.
•	Contract type is the biggest driver. Monthly-contract subscribers churned at 55.6%, against 8.3% for annual contracts. That's about 6.7× higher.
•	Most churn came from the Basic plan, so the revenue impact is limited.
•	Churn peaked in September 2024. Karnataka was the most affected state.
•	Average tenure is 1,451 days and ARPU is ₹18.8.
•	Revenue impact: about ₹74/month of ₹395 total monthly revenue was lost to churn (~18%), along with ₹2,047 in lost CLTV.
•	Customers with escalated support interactions were over-represented among churners.
Recommendations
1.	Look into Karnataka. Check for price changes, a rise in complaints or technical issues in the region.
2.	Review Basic plan changes in September. Were prices raised, or the plan changed, around the churn spike?
3.	Push monthly subscribers onto annual contracts. Given the 55.6% vs 8.3% gap, migrating contracts is the strongest retention lever.
4.	Watch competitors. At least one cancellation was a switch to a competitor.
5.	Contact high- and medium-risk customers first. Rank them by CLTV and open complaints, then reach out by email, SMS or call to fix their issues.

