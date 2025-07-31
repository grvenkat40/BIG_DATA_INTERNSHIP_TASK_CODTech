# Task 1 – Data Cleaning & Preparation

Welcome, machi! This README explains everything you need to replicate **Task 1**: cleaning the raw Kaggle dataset so it’s ready for analysis in Task 2.

---

## 📂 Project Structure

```
My_projects/
│
├── Finance_Input_Pyspark/
│   ├── card_data.csv             # original Kaggle CSV(s)
│   └── user_data.csv
|  
│── Finance_card_cleaned_Data/
│    |---part 0000 .csv
|
|── Finance_User_cleaned_Data/
|    |--part 0000.csv
|
│── Task_1_Data_clean_pyspark.py   # Spark job for Task 1
|
└── README_Task1.md      # ← this file
```



## 🔧 Prerequisites

| Tool                      | Recommended Version | Notes                                                            |
| ------------------------- | ------------------- | ---------------------------------------------------------------- |
| Java                      | **11 LTS**          | `JAVA_HOME` → `C:\Program Files\Java\jdk‑11`                     |
| Apache Spark              | **3.4.x**           | Stand‑alone install; add `%SPARK_HOME%\bin` to `Path`            |
| Hadoop WinUtils (Windows) | 3.2.2               | Place `winutils.exe` in `C:\hadoop‑3.2.2\bin`; set `HADOOP_HOME` |
| Python                    | 3.10+               | `pip install pyspark findspark pandas`                           |

> **Environment variables** (System → Advanced → Environment Variables)
>
> ```
> JAVA_HOME  = C:\Program Files\Java\jdk‑11
> HADOOP_HOME = C:\hadoop‑3.2.2
> SPARK_HOME  = C:\spark‑3.4.3
> Path += %JAVA_HOME%\bin;%HADOOP_HOME%\bin;%SPARK_HOME%\bin
> ```



## 🏃‍♂️ Running Task 1

### Option A – Command‑line

```bash
spark-submit scripts/task1_clean.py \
    --input data/raw/finance_raw.csv \
    --output data/cleaned/cleaned_data.csv
```

### Option B – Jupyter Notebook

1. `import findspark, os; findspark.init()`
2. Run the cells in `task1_clean.ipynb` (same logic as the script).



## 🧹 Cleaning Steps Implemented

| Step | Transformation                                                                                                        |
| ---- | --------------------------------------------------------------------------------------------------------------------- |
| 1    | **Load** raw CSV with `header=True`, `inferSchema=True`                                                               |
| 2    | **Currency cleanup** – remove `$` and `,` from `per_capita_income` using `regexp_replace`, then cast to `IntegerType` |
| 3    | **Date parsing** – convert `expires`/`date` strings to `TimestampType` via `to_timestamp()`                           |
| 4    | **Null handling** – counted nulls per column; dropped or imputed where required                                       |
| 5    | **Column pruning / renaming** – kept only relevant features and renamed to snake\_case                                |
| 6    | **Write** cleaned DataFrame with `coalesce(1)` + `mode("overwrite")` to the `data/cleaned` folder                     |



## ✅ Expected Output

- `data/cleaned/cleaned_data.csv` (single file)
- Sample schema:
  ```
  root
   |-- state: string                       (nullable = true)
   |-- per_capita_income: integer          (nullable = true)
   |-- expires: timestamp                  (nullable = true)
   |-- year: integer                       (nullable = true)
  ```



## 🛠 Troubleshooting Tips

| Symptom                              | Fix                                                           |
| ------------------------------------ | ------------------------------------------------------------- |
| `JavaPackage object is not callable` | Confirm Java 11 and `%JAVA_HOME%` set, restart kernel         |
| `Py4JJavaError` when writing         | Use raw string paths (`r"D:\…"`), avoid OneDrive sync folders |
| `winutils.exe` not found             | Ensure `C:\hadoop‑3.2.2\bin` in `Path` & file present         |


