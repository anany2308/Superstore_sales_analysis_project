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


### 8. Regional Performance Analysis
```python
region_analysis = module.groupby('Region', as_index=False)[['Sales', 'Profit']].sum()

region_analysis['Profit_Ratio'] = region_analysis['Profit'] / region_analysis['Sales']

region_analysis = region_analysis.sort_values(by='Sales', ascending=False)

display(region_analysis)

fig1 = px.bar(region_analysis, x='Region', y='Sales', title='Sales by Region')
fig1.show()

fig2 = px.bar(region_analysis, x='Region', y='Profit', title='Profit by Region')
fig2.show()
```
**Objective:** To identify top and underperforming regions based on sales and profitability.


### 9. Sales to Profit Ratio Analysis
```python
ratio_analysis = module.groupby('Category', as_index=False)[['Sales', 'Profit']].sum()

ratio_analysis['Profit_Ratio'] = ratio_analysis['Profit'] / ratio_analysis['Sales']

ratio_analysis = ratio_analysis.sort_values(by='Profit_Ratio')

display(ratio_analysis)

fig = px.bar(ratio_analysis, x='Category', y='Profit_Ratio',
             title='Sales to Profit Ratio by Category')
fig.show()
```
**Objective:** To evaluate profitability efficiency across product categories.

### 10. Discount Impact on Profit
```python
discount_analysis = module.groupby('Discount', as_index=False)[['Sales', 'Profit']].sum()

discount_analysis = discount_analysis.sort_values(by='Discount')

display(discount_analysis)

fig = px.scatter(module, x='Discount', y='Profit',
                 title='Discount vs Profit',
                 trendline='ols')
fig.show()
```
**Objective:** To analyze the relationship between discount levels and profit.


### 11. Customer Segment Profitability
```python
segment_analysis = module.groupby('Segment', as_index=False)[['Sales', 'Profit']].sum()

segment_analysis['Profit_Ratio'] = segment_analysis['Profit'] / segment_analysis['Sales']

segment_analysis = segment_analysis.sort_values(by='Profit', ascending=False)

display(segment_analysis)

fig = px.bar(segment_analysis, x='Segment', y='Profit',
             title='Profit by Customer Segment')
fig.show()
```
**Objective:** To identify the most valuable and least profitable customer segments.


### 12. Pareto Analysis (Top vs Bottom Products)
```python
product_analysis = module.groupby('Product Name', as_index=False)[['Sales', 'Profit']].sum()

product_analysis = product_analysis.sort_values(by='Sales', ascending=False)

product_analysis['Cumulative_Sales'] = product_analysis['Sales'].cumsum()

product_analysis['Cumulative_Percentage'] = (
    product_analysis['Cumulative_Sales'] / product_analysis['Sales'].sum()
) * 100

display(product_analysis.head(10))

top_products = product_analysis.head(50)

fig = px.line(top_products,
              x=top_products.index,
              y='Cumulative_Percentage',
              title='Pareto Analysis (Top Products Contribution)')
fig.show()
```
**Objective:** To identify key products driving the majority of revenue.

## Findings and Conclusion  

- **Monthly Sales Trends:** Sales vary across months, indicating seasonal demand patterns with certain months generating significantly higher revenue.  

- **Sales vs Profit Gap:** High sales do not always result in high profit, suggesting the impact of discounts, costs, or low-margin products.  

- **Category Performance:** Some categories contribute the majority of sales, while others consistently underperform and require strategic improvement.  

- **Sub-Category Insights:** A few sub-categories dominate sales and profit, whereas others generate low revenue or even losses.  

- **Customer Segment Analysis:** Certain customer segments contribute more to both sales and profit, making them key targets for business growth.  

- **Profit Distribution:** Profit is unevenly distributed, highlighting that not all high-selling products are profitable.  

- **Sales-to-Profit Efficiency:** Variations in the sales-to-profit ratio indicate inefficiencies in pricing or cost management.
  
- **Discount Impact:** Higher discounts negatively affect profitability, with excessive discounting leading to losses.

- **Pareto Effect:** A small proportion of products contribute to the majority of total sales and profit.



This analysis provides a comprehensive understanding of sales performance and profitability. It highlights key areas for improvement, such as optimizing low-performing products, focusing on high-value customer segments, and improving profit margins to drive better business decisions.
