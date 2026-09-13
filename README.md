# Data-Ingestion-Cleaning-Processing

Warehouse Data Cleaning & Preprocessing with Pandas

A practical data-cleaning project that transforms messy warehouse
inventory data into a reliable, analysis-ready dataset using Python
and Pandas.

📌 Overview

Real-world business data rarely arrives in perfect condition. Warehouse
and inventory datasets can contain missing values, inconsistent text,
incorrect data types, and unusual numerical values that can affect
analysis and decision-making.

This project demonstrates an end-to-end data ingestion, cleaning,
preprocessing, validation, and feature engineering workflow using
Pandas. The raw warehouse dataset is inspected, its quality issues
are identified, appropriate cleaning techniques are applied, and the
final standardized dataset is exported for further analysis.

The focus is on making the process reproducible, explainable, and
practical rather than simply applying transformations without
understanding the data.

🎯 Objectives

Load and inspect a raw warehouse inventory dataset using Pandas.

Identify and handle missing values.

Detect and correct inconsistent data types.

Standardize text fields and formatting.

Check and remove genuine duplicate records.

Identify potential numerical outliers.

Apply suitable data-imputation techniques.

Perform meaningful feature engineering.

Compare the dataset before and after cleaning.

Export the cleaned dataset as clean_dataset.csv.

🗂️ Dataset

The dataset represents warehouse inventory information covering
products, categories, warehouse locations, stock quantities, prices,
suppliers, inventory status, and restocking dates.

Columns

Column             Description

Product ID       Product reference identifier
Product Name     Name of the inventory product
Category         Product category
Warehouse        Warehouse where the item is stored
Location         Storage/location information
Quantity         Available inventory quantity
Price            Unit price of the product
Supplier         Supplier associated with the product
Status           Current inventory status
Last Restocked   Date of the most recent restocking

Data Quality Issues

The raw dataset contains realistic issues such as:

Missing values in Quantity, Price, and Last Restocked

Unnecessary whitespace in text values

Inconsistent capitalization in categorical fields

Numeric values represented as text

Dates requiring conversion to a proper datetime format

Potential numerical outliers

Duplicate records requiring validation

The supplied dataset currently contains 1,000 records and 10 original
columns. The workflow is designed to scale to larger datasets,
including the 10,000+ row requirement specified by the assignment.

🔄 Project Workflow

Raw Warehouse Dataset
        ↓
Data Ingestion
        ↓
Initial Inspection
        ↓
Data Quality Assessment
        ↓
Missing Values ─┐
Data Types     ├──→ Cleaning & Standardization
Text Issues    │
Duplicates     │
Outliers       ┘
        ↓
Feature Engineering
        ↓
Validation & Before/After Comparison
        ↓
Clean Dataset
        ↓
clean_dataset.csv

🛠️ Technologies Used

Python

Pandas -- data ingestion, cleaning, transformation, and analysis

NumPy -- numerical operations

Matplotlib -- optional visual exploration

Jupyter Notebook -- interactive development and documentation

🧹 Data Cleaning Approach

1. Data Ingestion

The raw CSV is loaded into a Pandas DataFrame:

import pandas as pd

df = pd.read_csv("warehouse_messy_data(1).csv")

2. Initial Inspection

The dataset is examined using head(), info(), describe(), and
shape() to understand its initial structure and quality.

3. Missing Value Handling

Missing values are identified using:

df.isnull().sum()

Numerical fields such as Quantity and Price can be imputed using an
appropriate statistical value such as the median. Missing restocking
dates are treated carefully rather than inventing unsupported dates.

4. Data Type Correction

Text-form numerical values such as "two hundred" are converted into
numeric values before the Quantity column is standardized.

The Last Restocked column is converted into Pandas datetime format so
that it can be analyzed reliably.

5. Text Standardization

Unnecessary spaces and inconsistent capitalization are cleaned:

df["Product Name"] = df["Product Name"].str.strip().str.title()

Similar standardization is applied to relevant categorical fields.

6. Duplicate Validation

Exact duplicate records are identified with:

df.duplicated().sum()

Only genuine duplicate rows are removed. Repeated product IDs are not
automatically treated as duplicates because the same product can
legitimately appear across different inventory records.

7. Outlier Analysis

Numerical columns such as Quantity are examined using the
Interquartile Range (IQR) method.

Potential outliers are investigated rather than automatically deleted
because an unusually large inventory quantity may still be a valid
business value.

📊 Feature Engineering

The cleaned data is enhanced with useful derived features.

Inventory Value

df["Inventory Value"] = df["Quantity"] * df["Price"]

This estimates the total inventory value represented by each record.

Stock Score

status_mapping = {
    "In Stock": 1,
    "Low Stock": 0.5,
    "Out of Stock": 0
}

df["Stock Score"] = df["Status"].map(status_mapping)

Restock Year

df["Restock Year"] = df["Last Restocked"].dt.year

These features make the dataset more useful for future inventory
analysis and visualization.

✅ Validation

The final dataset is validated by comparing important quality indicators
before and after cleaning:

Number of rows

Number of columns

Total missing values

Duplicate records

Data types

Numerical ranges

Newly created features

This ensures that the cleaning process improves data quality without
unnecessarily removing valid information.

📁 Project Structure

warehouse-data-cleaning/
│
├── warehouse_messy_data(1).csv     # Raw dataset
├── Warehouse_Data_Cleaning.ipynb   # Main Jupyter Notebook
├── clean_dataset.csv               # Cleaned dataset
└── README.md                       # Project documentation

🚀 How to Run

1. Clone the repository

git clone <your-repository-link>
cd warehouse-data-cleaning

2. Install dependencies

pip install pandas numpy matplotlib jupyter

3. Start Jupyter Notebook

jupyter notebook

Open Warehouse_Data_Cleaning.ipynb and run the cells from top to
bottom.

The cleaned dataset will be generated as:

clean_dataset.csv

📈 Expected Outcome

The final output is a clean and standardized warehouse dataset suitable
for:

Inventory analysis

Stock monitoring

Product-level analysis

Supplier analysis

Inventory value calculations

Restocking analysis

Data visualization

Future machine-learning workflows

The project demonstrates a documented and reproducible preprocessing
pipeline, not just a cleaned CSV file.

💡 Key Learning Outcomes

Working with messy real-world data

Data quality assessment

Missing-value treatment

Data type conversion

Text normalization

Duplicate detection

Outlier analysis

Feature engineering

Data validation

Reproducible Pandas workflows

🔮 Future Improvements

Scale the dataset to 10,000+ records.

Add automated data-quality reports.

Build inventory dashboards using Power BI.

Add supplier performance analysis.

Create low-stock alerts.

Automate the cleaning pipeline for newly uploaded files.

Add tests for critical cleaning rules.

👤 Author

Nivetha L
B.Tech Computer Science Engineering

This project was developed as a practical exercise in data ingestion,
cleaning, preprocessing, and feature engineering using Pandas.

📄 License

This project is intended for educational and portfolio purposes.
