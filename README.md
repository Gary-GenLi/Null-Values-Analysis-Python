# Python-Null-Values-Data-Cleansing
# Table of Contents
- [1. Introduction](#1-introduction)
- [2. Project Overview](#2-project-overview)
- [3. Key Features](#3-key-features)
- [4. Code Highlights](#4-code-highlights)
- [5. Lessons Learned](#5-lessons-learned)

## 1. Introduction

In data analysis, ensuring the completeness and accuracy of datasets is essential. Missing values can significantly affect the quality of analysis, making it crucial to identify and manage them effectively. This script is designed to analyze null values in a CSV file, providing insights into their distribution and helping with the data cleaning process.

## 2. Project Overview

The CSV Null Value Analysis Script performs the following tasks:
1. **Import Data**: Reads a CSV file into a DataFrame.
2. **Select Columns**: Chooses columns for analysis, excluding non-essential ones.
3. **Analyze Null Values**: Computes the number of null values per row and lists columns with null values.
4. **Filter Data**: Keeps only columns related to null values for further examination.
5. **Export Results**: Saves the analyzed data to a new CSV file.

## 3. Key Features

- **Column Filtering**: Selects only the relevant columns for null value analysis.
- **Null Value Counting**: Calculates the total number of null values in each row.
- **Null Value Listing**: Lists columns with null values for each row.
- **Data Export**: Outputs results to a CSV file, appending data to avoid overwriting.
- **Performance Tracking**: Measures and prints the execution time of the script.

## 4. Code Highlights

### Selecting Columns

```python
df_sel_columns = df.columns[2:]
df = df[df_sel_columns]
```
- **Purpose**: Excludes the first two columns from the DataFrame and keeps the remaining ones for analysis. This step focuses the script on the relevant data fields.

### Inserting Columns Related to Null Values

```python
df.insert(0, 'CountofNullColumns', df.isnull().sum(axis='columns'))
df.insert(0, 'ListofNullColumns', df.isnull().dot(df.columns + ',').str[:-1].str.split(',').apply(lambda x:', '.join(x)))
```
- **Count of Null Columns**: df.isnull().sum(axis='columns') calculates the number of null values in each row. This count is inserted as CountofNullColumns for easy reference.
- **List of Null Columns**: The script generates a comma-separated list of columns with null values using df.isnull().dot(df.columns + ',') and formats it with .str.split(',') and .apply(lambda x:', '.join(x)). This is inserted as ListofNullColumns.

### Filtering Columns
```python
df_sel_columns = df.columns[0:2]
df = df[df_sel_columns]
```
- **Purpose**: After adding columns for null value analysis, this step retains only CountofNullColumns and ListofNullColumns, ensuring the final DataFrame focuses on the null value summary.

## 5. Lessons Learned
- **DataFrame Operations**: Using pandas methods like isnull(), sum(), and dot() effectively helps in summarizing null values. These methods streamline data analysis and provide insights into data completeness.
- **Column Manipulation**: Adding new columns with information derived from existing data using insert() is a powerful technique. It enhances the DataFrame with additional insights while preserving the original structure.
- **Readability and Maintenance**: Breaking down complex operations into clear steps improves code readability and maintainability. Documenting each step helps in understanding and modifying the script in the future.
- **Performance Considerations**: For large datasets, consider performance implications. Monitoring execution time and optimizing data processing can help manage large volumes of data efficiently.
