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
import pandas as pd

import plotly.express as px
import plotly.graph_objects as go
import plotly.io as pio
import plotly.colors as colors 

pio.templates.default = "plotly_white"


## 📊 Business Problems and Solutions  

### 1. Monthly Sales Analysis  

```python
monthly_sales = data.groupby('Order Month')['Sales'].sum().sort_values()

highest_month = monthly_sales.idxmax()
lowest_month = monthly_sales.idxmin()

print(monthly_sales)
print("Highest Sales Month:", highest_month)
print("Lowest Sales Month:", lowest_month)
