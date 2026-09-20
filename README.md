# Python Data Cleaning and Analysis Project

## 📌 Project Overview

This project focuses on cleaning, analyzing, and visualizing an employee dataset using Python.

The main objective is to identify and handle common data-quality problems such as missing values, duplicate records, inconsistent text formatting, and potential outliers.

The cleaned dataset was then visualized and exported into Excel and CSV formats.

---

## 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Jupyter Notebook
* Excel

---

## 📂 Dataset

The original dataset was provided as an Excel file:

`sample_data_cleaning_project.xlsx`

The dataset contains the following columns:

* `Name`
* `Age`
* `Salary`
* `Join_Date`
* `Department`

---

# 🔍 Project Workflow

## 1. Import Required Libraries

The following Python libraries were imported:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

---

## 2. Load the Dataset

The Excel dataset was loaded using Pandas:

```python
df = pd.read_excel("sample_data_cleaning_project.xlsx")
```

---

## 3. Explore the Dataset

The dataset was inspected using:

```python
df.head()
df.shape
df.info()
df.columns
```

The original dataset contained:

* **43 rows**
* **5 columns**

---

## 4. Check Missing Values

Missing values were identified using:

```python
df.isnull().sum()
```

Missing values were found in:

* Age
* Salary

---

## 5. Check Duplicate Records

Duplicate records were identified using:

```python
df.duplicated().sum()
```

One duplicate record was found.

It was removed using:

```python
df = df.drop_duplicates()
```

---

## 6. Handle Missing Age Values

The median Age was calculated and used to replace missing Age values.

```python
df['Age'] = df['Age'].fillna(df['Age'].median())
```

After cleaning, there were no missing Age values.

---

## 7. Handle Missing Salary Values

The median Salary was used to replace missing Salary values.

```python
df['Salary'] = df['Salary'].fillna(df['Salary'].median())
```

After cleaning, there were no missing Salary values.

---

## 8. Investigate Salary Outliers

The Salary column was analyzed using:

```python
df['Salary'].describe()
```

Some salaries were much higher than the normal salary range.

Instead of automatically deleting these values, they were investigated as potential outliers.

---

## 9. Detect Outliers Using IQR

The Interquartile Range (IQR) method was used.

```python
Q1 = df['Salary'].quantile(0.25)
Q3 = df['Salary'].quantile(0.75)

IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR
```

The calculated upper bound was approximately:

**₹98,802.50**

Salaries above this value were considered potential outliers.

---

## 10. Create an Outlier Flag

A new column called `Salary_Outlier` was created.

```python
df['Salary_Outlier'] = (
    (df['Salary'] < lower_bound) |
    (df['Salary'] > upper_bound)
)
```

This allowed potential outliers to be identified without deleting the original salary values.

### Outlier handling approach

The project follows:

**Detect → Flag → Review → Preserve unless proven incorrect**

A statistical outlier is not automatically a data-entry error.

---

# 🔤 Data Type and Text Cleaning

## 11. Check Data Types

The data types of all columns were checked using:

```python
df.dtypes
```

The dataset contains:

* Name → Text
* Age → Numeric
* Salary → Numeric
* Join_Date → Date/Time
* Department → Text
* Salary_Outlier → Boolean

---

## 12. Verify Date Format

The `Join_Date` column was converted/verified as a datetime column:

```python
df['Join_Date'] = pd.to_datetime(df['Join_Date'])
```

---

## 13. Check Department Values

Department values were checked using:

```python
df['Department'].value_counts()
```

The dataset contains:

* HR
* Finance
* IT

---

## 14. Check Text Consistency

Department and Name values were checked for unnecessary spaces and formatting issues.

```python
df['Department'].unique()
df['Name'].str.strip().unique()
```

---

## 15. Clean Text Columns

Unnecessary leading and trailing spaces were removed:

```python
df['Name'] = df['Name'].str.strip()
df['Department'] = df['Department'].str.strip()
```

---

# 📊 Data Visualization

Four visualizations were created to understand the cleaned dataset.

## 16. Department Distribution

A count plot was created to show the number of employees in each department.

```python
sns.countplot(data=df, x='Department')
```

The distribution was:

* HR → 22
* Finance → 10
* IT → 10

---

## 17. Salary Distribution

A histogram was created to understand the salary distribution.

```python
sns.histplot(data=df, x='Salary', bins=15, kde=True)
```

The visualization showed a concentration of salaries in the lower range and a long right tail caused by unusually high salary values.

---

## 18. Age Distribution

An age histogram was created:

```python
sns.histplot(data=df, x='Age', bins=10, kde=True)
```

The ages ranged approximately from **21 to 57**.

---

## 19. Salary Boxplot

A boxplot was created to visualize potential salary outliers:

```python
sns.boxplot(x=df['Salary'])
```

The boxplot visually showed the unusually high salary values.

---

# ✅ Final Data Validation

## 20. Missing Value Check

```python
df.isnull().sum()
```

Result:

**0 missing values**

---

## 21. Duplicate Check

```python
df.duplicated().sum()
```

Result:

**0 duplicate rows**

---

## 22. Final Dataset Size

```python
df.shape
```

Final dataset:

**42 rows × 6 columns**

The dataset changed from:

**43 rows × 5 columns**

to:

**42 rows × 6 columns**

because:

* 1 duplicate row was removed
* 1 `Salary_Outlier` column was added

---

## 23. Final Data Quality Report

The following checks were performed:

```python
print("Rows:", df.shape[0])
print("Columns:", df.shape[1])
print("Missing values:", df.isnull().sum().sum())
print("Duplicate rows:", df.duplicated().sum())
print("Potential salary outliers:", df['Salary_Outlier'].sum())
```

Final results:

| Check                     | Result |
| ------------------------- | -----: |
| Rows                      |     42 |
| Columns                   |      6 |
| Missing Values            |      0 |
| Duplicate Rows            |      0 |
| Potential Salary Outliers |      6 |

---

# 💾 Exported Files

The cleaned dataset was exported into two formats.

### Excel

```python
df.to_excel("cleaned_employee_data.xlsx", index=False)
```

Output:

`cleaned_employee_data.xlsx`

### CSV

```python
df.to_csv("cleaned_employee_data.csv", index=False)
```

Output:

`cleaned_employee_data.csv`

---

# 📈 Final Results

After completing the data-cleaning process:

* Duplicate records were removed.
* Missing Age values were handled using the median.
* Missing Salary values were handled using the median.
* Date formatting was verified.
* Text columns were checked and cleaned.
* Salary outliers were detected using the IQR method.
* Six potential salary outliers were flagged.
* No records were deleted solely because they were statistical outliers.
* Four visualizations were created.
* The final dataset contains 42 rows and 6 columns.
* The cleaned dataset was exported as both Excel and CSV files.

---

# 🎯 Conclusion

This project demonstrates a basic end-to-end data-cleaning workflow using Python.

The dataset was inspected, cleaned, analyzed, visualized, validated, and exported into usable formats.

The project also demonstrates why outliers should be investigated rather than automatically removed. Statistical methods can identify unusual observations, but additional information is needed to determine whether an observation is actually incorrect.

---

## 👨‍💻 Skills Demonstrated

* Python programming
* Pandas
* NumPy
* Data cleaning
* Missing-value handling
* Duplicate detection
* Data validation
* Outlier detection using IQR
* Data visualization
* Excel data processing
* CSV data processing
* Basic exploratory data analysis
