# Lab 6: Association Rule Mining with Apriori and FP-Growth
Avijit Saha  
Advanced Big Data and Data Mining (MSCS-634-M20)  
Dr. Satish Penmatsa  
March 18, 2026  

## This Repo is Lab 6: Association Rule Mining with Apriori and FP-Growth, Advanced Big Data and Data Mining (MSCS-634-M20)

## Project Overview
This lab explores the implementation and comparative analysis of Association Rule Mining techniques. Using the **Online Retail Dataset**, we identify frequent itemsets and generate association rules to uncover hidden purchasing patterns. The project evaluates two primary algorithms—**Apriori** and **FP-Growth**—to determine their efficiency and effectiveness in a real-world retail context.

## Key Objectives
* **Data Preprocessing:** Cleaning 500k+ rows of transactional data and transforming it into a one-hot encoded boolean matrix.
* **Pattern Discovery:** Identifying items frequently bought together using a 3% support threshold.
* **Rule Generation:** Extracting actionable insights using Support, Confidence, and Lift metrics.
* **Performance Comparison:** Benchmarking the execution time of candidate-based (Apriori) vs. tree-based (FP-Growth) mining.

## Dataset
The analysis was performed on the **Online Retail Dataset**, which contains transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based non-store online retail.
* **Format:** .xlsx (Excel)
* **Key Features:** InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID.

## Key Insights & Association Rules
The mining process revealed strong "Collector" and "Set-based" purchasing behaviors:

| Antecedent | Consequent | Support | Confidence | Lift |
| :--- | :--- | :--- | :--- | :--- |
| PINK REGENCY TEACUP | GREEN REGENCY TEACUP | 0.0307 | 0.8263 | **16.77** |
| ROSES REGENCY TEACUP | GREEN REGENCY TEACUP | 0.0372 | 0.7204 | **14.62** |
| ALARM CLOCK BAKELIKE RED | ALARM CLOCK BAKELIKE GREEN | 0.0310 | 0.6089 | **12.80** |

**Interpretation:** Customers who purchase a specific color of a "Regency Teacup" have an 82.6% probability of purchasing the matching green variant. The Lift of 16.77 suggests these items are highly dependent, making them perfect candidates for product bundling.

## Comparative Analysis
| Algorithm | Execution Time |
| :--- | :--- |
| **Apriori** | **0.1758 seconds** |
| **FP-Growth** | **1.5059 seconds** |

**Conclusion:** In this specific environment, **Apriori outperformed FP-Growth**. While FP-Growth is generally faster for dense datasets, the sparse nature of retail data combined with a conservative support threshold allowed Apriori to prune the search space faster than the time required for FP-Growth to construct its initial FP-Tree.

## Visualizations
The project includes the following Seaborn-powered visualizations:
1. **Top 10 Frequent Items:** A barplot identifying the most common individual products.
2. **Item Co-occurrence Heatmap:** Visualizing the correlation between the top 15 items.
3. **Confidence vs. Lift Scatter Plot:** Identifying high-strength rules (Top-Right quadrant).

## Challenges & Resolutions
* **Unicode/Format Error:** Resolved a `UnicodeDecodeError` by switching to `pd.read_excel` with the `openpyxl` engine.
* **Memory Management:** Handled high-dimensionality data by filtering out "C" (Cancelled) transactions and converting the basket matrix to `bool` type to optimize RAM and satisfy `mlxtend` requirements.

## How to Run
1. Ensure you have the following libraries installed: `pandas`, `mlxtend`, `seaborn`, `openpyxl`.
2. Place the `Online Retail.xlsx` file in the specified directory.
3. Run the Jupyter Notebook cells sequentially.
