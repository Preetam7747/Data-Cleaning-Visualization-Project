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


## Data Cleaning
The dataset was cleaned by:
- Handling missing values
- Removing duplicate records
- Filling missing Age and Salary values
- Checking for salary outliers


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


# 🎯 Conclusion

This project demonstrates a basic end-to-end data-cleaning workflow using Python.

The dataset was inspected, cleaned, analyzed, visualized, validated, and exported into usable formats.

The project also demonstrates why outliers should be investigated rather than automatically removed. Statistical methods can identify unusual observations, but additional information is needed to determine whether an observation is actually incorrect.

---
