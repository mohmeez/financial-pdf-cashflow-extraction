# Financial PDF Data Extraction & Cash Flow Analysis (Python)

### Project Overview

This project demonstrates how to extract structured financial data from multi-page PDF statements using Python, transform it into analyzable tabular data, and compute derived financial metrics such as net cash flow and running balances.

The PDF used in this project simulates 12 accounts, each with its own Statement of Cash Flows across 12 pages, similar to real-world bank, treasury, or fund statements that analysts encounter in practice.

----------------Extract Data from this PDF (12 accounts with each account summary------------

![pdf_sample](https://github.com/user-attachments/assets/4f8e81b8-2aa3-4c8e-9119-9ccc92d561c5)


----------------------And create data frames using pandas for feature Engineering----------------------------------------------
<img width="1202" height="976" alt="image" src="https://github.com/user-attachments/assets/875570cc-f528-4013-9665-7ff649a53a0f" />

----------------------------------------------Excel output------------------------------------------------------------------------
<img width="1272" height="1043" alt="image" src="https://github.com/user-attachments/assets/d3e03eb4-ada8-44f1-85fa-0ea3464a8710" />




### This project is designed to showcase:

PDF data extraction

Data cleaning and validation

Financial computations

Practical pandas usage for accounting-style workflows

## 📂 Data Description

Each page of the PDF represents one account and contains:

1. Account Summary Section

* Opening Cash

* Total Inflows
* Total Outflows
* Net Change in Cash
* Ending Cash

2. Transactions Table

* Column	Description
* Date	Transaction date
* Description	Transaction details
* Category	Type of transaction
* Inflow	Cash received
* Outflow	Cash paid


## Technologies Used

Python

pandas – data manipulation & analysis

pdfplumber – PDF text and table extraction

NumPy – numerical operations

## Project Workflow

# Step 1: Extract Data from PDF

* Loop through all PDF pages

* Extract account identifiers

Parse:

Summary tables

Transaction tables

Store extracted data in pandas DataFrames

# Step 2: Data Cleaning

* Convert monetary values to numeric format

* Parse dates

* Sort transactions chronologically by account

# Step 3: Feature Engineering (New Columns)

The following four computed columns are created:

### Column	Descriptions (Formulas)

Net Cash Flow ---> Inflow - Outflow
Running Balance ----> Cumulative cash position per account
Outflow % -----> Share of each transaction relative to total account outflows
Large Transaction Flag -----> Flags transactions above a defined threshold 

### Key Financial Calculations

* Net Cash Flow:
df_txn["Net Cash Flow"] = df_txn["Inflow"] - df_txn["Outflow"]

* Running Balance
df_txn["Running Balance"] = (
    df_txn.groupby("Account")["Net Cash Flow"].cumsum()
    + df_txn["Opening Cash"]
)

* Outflow Percentage
df_txn["Outflow %"] = df_txn["Outflow"] / df_txn.groupby("Account")["Outflow"].transform("sum")

### 📁 Output Files

extracted_with_computed_columns.csv
→ Cleaned transaction-level data with computed financial metrics

extracted_summaries.csv
→ Account-level cash flow summaries

### These outputs are ready for:

Financial analysis

Reconciliation

Visualization

Reporting dashboard

# Run This Project Locally
1) Clone the repository
git clone https://github.com/mohmeez/financial-pdf-cashflow-extraction
cd financial-pdf-cashflow-extraction

2) Create and activate a virtual environment

Windows (PowerShell)
python -m venv .venv
.\.venv\Scripts\Activate


Mac/Linux:
python3 -m venv .venv
source .venv/bin/activate

3) Install dependencies
pip install --upgrade pip
pip install -r requirements.txt

4) Run the project
Option A: Run the notebook (recommended)
jupyter notebook


Then open:

data_extraction.ipynb

Run the cells top to bottom.

Option B: If you later add a Python script (recommended for production)

If you create a script like extract_cashflows.py, then run:

python extract_cashflows.py

5) Outputs

After running, the project generates extracted files such as:

extracted_summaries.xlsx
extracted_with_computed_columns.xlsx
(or CSV versions if you save as CSV)

If you've made it this far, Kudos!!
Happpy Extracting :)
