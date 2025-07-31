# 🧾 README: Apache Spark Task 2 - Data Analysis

## 📌 Task Description

**Objective:** Use Apache Spark to analyze a large dataset by implementing the following operations:

- Filtering
- Grouping
- Aggregations

**Deliverable:** A Spark job script along with output showing the results of the analysis.

---

## 🧰 Prerequisites

- Apache Spark installed and configured
- Java JDK 11 set as JAVA\_HOME
- Dataset cleaned and saved from Task 1 (e.g., `cleaned_finance_data.csv`)
- PySpark configured and working in your environment

---

## 📂 Files Structure

```bash
BIG_Data_Tast_2/
|
├── task2_analysis.py
├── output/
│   └── Finance_Card_cleaned.csv
|   └── Finance_User_cleaned.csv
└── README_task2.md
```

---

## 🧼 Dataset Used

- File: `cleaned_finance_data.csv`
- Format: CSV
- Columns: `card_type`, `card_brand`, `expires`, `retirement_age`, `per_capita_income`, etc.

---

## 🧪 Operations Performed

### 1. Filtering

```python
# Example: Filter only credit cards that are Mastercard
filtered_df = df.filter((df.card_type == "Credit") & (df.card_brand == "Mastercard"))
```

### 2. Grouping and Aggregation

```python
from pyspark.sql.functions import avg, count, max, min

# Example: Average retirement age
df.select(avg("retirement_age")).show()

# Group by card_type and find average per capita income
df.groupBy("card_type").agg(avg("per_capita_income").alias("avg_income")).show()
```

---

## 📝 Output

- Output saved as CSV: `output/analysis_results.csv`
- Format: Human-readable aggregated results

---

## ▶️ How to Run

```bash
spark-submit task2_analysis.py
```

---

## ✅ Completion

-

---

## 📞 Contact

Prepared by: **Venkat**

For questions or feedback, feel free to reach out!

