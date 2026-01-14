# Electra_Financial_Data
Electra Consumer Products: Financial Data Pipeline &amp; Analysis (2022-2025)
Project Overview
This project is an end-to-end ETL (Extract, Transform, Load) and Analysis pipeline analyzing the financial performance of Electra Consumer Products (ECP), a leading Israeli retail and electrical appliance company.

The goal was to convert unstructured financial data locked in complex PDF reports (with Hebrew text issues) into a structured SQL database to analyze revenue trends, seasonality, and profitability margins.

🎯 Key Objectives
Automated Extraction: Extract key financial metrics (Revenue, Gross Profit) from quarterly and annual PDF reports.

Hebrew Text Handling: Solve challenges related to "Visual Hebrew" (RTL text reversed in PDF extraction).

Data Engineering: Clean, normalize, and load data into a SQLite database.

Business Intelligence: Analyze seasonality (Summer vs. Winter) and profitability trends using SQL and Python.

🛠️ Tech Stack
Language: Python

Libraries: pdfplumber (PDF parsing), pandas (Data manipulation), sqlite3 (Database management), matplotlib & seaborn (Visualization).

Database: SQLite (Embedded SQL engine).

Concepts: ETL, Regex (Regular Expressions), Data Cleaning, Financial Modeling.

⚙️ The Pipeline
1. Data Extraction (The Challenge)
Extracting data from Israeli financial reports is challenging due to:

Right-to-Left (RTL) text: Python libraries often read Hebrew backwards (e.g., "הכנסות" becomes "תוסנכה").

Unstructured Format: Tables vary between quarters and years.

Solution: I built a custom parser using pdfplumber and regex that:

Detects visual Hebrew keywords (reversed text).

Identifies the correct financial tables based on numerical context (filtering out page numbers/notes).

Extracts specific quarterly data points (Revenue, Gross Profit).

2. Data Transformation & Cleaning
Normalization: Merged actual data from 2025 reports with annual historical data (2022-2024).

Seasonality Modeling: For years where only annual totals were available, I applied a seasonality distribution model based on historical patterns (Q3 peak due to A/C sales) to estimate quarterly breakdowns.

Type Tagging: Added a Data_Type column to distinguish between 'Actual' (verified reports) and 'Estimate' (model-based) data.

3. Loading to SQL
The cleaned dataset was loaded into a SQLite database (electra.db) to enable SQL-based querying.

SQL

-- Example Table Structure
CREATE TABLE Electra_Revenue (
    Report_Date DATE,
    Year INT,
    Quarter VARCHAR(5),
    Revenue_Mil DECIMAL(10,2),
    Gross_Profit_Mil DECIMAL(10,2),
    Margin_Pct DECIMAL(5,3),
    Data_Source VARCHAR(50)
);
📈 Key Insights & Results
1. The "King" of Quarters: Q3 (Summer)
SQL analysis confirmed a strong seasonality trend. Q3 (July-Sept) is consistently the strongest quarter in both revenue and profitability.

Why? Peak season for air conditioner sales in Israel.

Data: Average Q3 revenue is ~1.96B NIS, significantly higher than Q1 (~1.54B NIS).

2. Revenue vs. Margin Efficiency
While Q4 (End of Year) shows high revenue (likely due to Black Friday/Holiday sales), it suffers from the lowest Gross Margin (~28.0%). This indicates a "volume over value" strategy during sales periods.

3. 2025 Performance
In 2025, the company showed an improvement in efficiency, with Gross Margins jumping to ~29.4% in Q3, compared to a historical average of ~28.3%.****
