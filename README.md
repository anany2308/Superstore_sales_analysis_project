# Superstore Sales Analysis using Python

![Superstore Logo](https://github.com/anany2308/Superstore_sales_analysis_project/blob/main/superstore%20logo.webp)

## Overview
This project analyzes an e-commerce dataset using Python in Jupyter Notebook to extract insights on sales, profit, and customer behavior. It focuses on identifying trends across months, product categories, sub-categories, and customer segments to support better business decisions.

## Objectives
- Analyze monthly sales and identify highest & lowest months.
- Compare sales across categories and sub-categories.
- Evaluate monthly profit and top-performing periods.
- Analyze profit by category and sub-category.
- Study sales and profit by customer segment.
- Calculate sales-to-profit ratio.

## Business Problems and Solutions

### Import Libraries
```python
import pandas as pd

import plotly.express as px
import plotly.graph_objects as go
import plotly.io as pio
import plotly.colors as colors 

pio.templates.default = "plotly_white"
```
### Load Dataset
```python
data = pd.read_csv("Sample - Superstore.csv", encoding='latin-1')
data.head()
```

### Statistical Summary
```python
data.describe()
```

### View Data
```python
data.head()
```

### Data Information
```python
data.info()
```

### Convert Date Columns
```python
data['Order Date'] = pd.to_datetime(data['Order Date'])
data['Ship Date'] = pd.to_datetime(data['Ship Date'])
```

### Feature Engineering (Date)
```python
data['Order Month'] = data['Order Date'].dt.month
data['Order Year'] = data['Order Date'].dt.year
data['Order Day of Week'] = data['Order Date'].dt.dayofweek
```


### 1. Monthly Sales Analysis
```python
monthly_sales = data.groupby('Order Month')['Sales'].sum().sort_values()

highest_month = monthly_sales.idxmax()
lowest_month = monthly_sales.idxmin()

print(monthly_sales)
print("Highest Sales Month:", highest_month)
print("Lowest Sales Month:", lowest_month)
```
**Objective:** Identify the months with highest and lowest sales.


### 2. Sales by Category
```python
category_sales = data.groupby('Category')['Sales'].sum().sort_values()

highest_category = category_sales.idxmax()
lowest_category = category_sales.idxmin()

print(category_sales)
print("Highest Category:", highest_category)
print("Lowest Category:", lowest_category)
```
**Objective:** Find best and worst performing product categories.



### 3. Sales by Sub-Category
```python
sub_category_sales = data.groupby('Sub-Category')['Sales'].sum().sort_values()

print(sub_category_sales)
```
**Objective:** Analyze detailed sales performance at sub-category level.


### 4. Monthly Profit Analysis
```python
monthly_profit = data.groupby('Order Month')['Profit'].sum()

highest_profit_month = monthly_profit.idxmax()

print(monthly_profit)
print("Highest Profit Month:", highest_profit_month)
```
**Objective:** Identify the most profitable month.


### 5. Profit by Category & Sub-Category
```python
profit_category = data.groupby('Category')['Profit'].sum().sort_values()
profit_sub_category = data.groupby('Sub-Category')['Profit'].sum().sort_values()

print(profit_category)
print(profit_sub_category)
```
**Objective:** Evaluate profitability across categories and sub-categories.



### 6. Sales & Profit by Customer Segment
```python
segment_analysis = data.groupby('Segment')[['Sales', 'Profit']].sum()

print(segment_analysis)
```
**Objective:** Understand performance across different customer segments.



### 7. Sales to Profit Ratio
```python
data['Sales_to_Profit_Ratio'] = data['Sales'] / data['Profit']

ratio_analysis = data[['Sales', 'Profit', 'Sales_to_Profit_Ratio']]

print(ratio_analysis.head())
```
**Objective:** Analyze efficiency of sales in generating profit.
