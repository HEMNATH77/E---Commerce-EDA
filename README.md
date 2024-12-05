# World-Education-EDA

# E-Commerce Data Analysis 2024

This project demonstrates an end-to-end exploratory data analysis (EDA) of an e-commerce dataset using Python. It includes steps to clean, filter, visualize, and analyze data to gain insights into sales, discounts, and payment methods.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Prerequisites](#prerequisites)
- [Code Walkthrough](#code-walkthrough)
- [Visualizations](#visualizations)
- [Results](#results)

---

## Project Overview
This project provides insights into the following aspects of an e-commerce dataset:
- Cleaning and transforming the dataset
- Identifying missing data and handling it
- Filtering and sorting data
- Grouping and aggregating data for detailed analysis
- Visualizing key metrics such as sales, discounts, and payment method distribution

---

## Dataset
The dataset used for this analysis is named **"E commerce 2024.csv"**. It contains the following columns:
- **Product Id**: Unique identifier for products (dropped in the analysis)
- **Price (Rs.)**: Original price of the product
- **Final_Price(Rs.)**: Price after applying discounts
- **Discount (%)**: Discount percentage applied
- **Category**: Product category
- **Payment_Method**: Payment methods used for transactions

---

## Prerequisites
To run this project, ensure you have the following installed:
- Python 3.7+
- Libraries:
  - `numpy`
  - `pandas`
  - `matplotlib`
  - `seaborn`

---



## Code Walkthrough

### Data Loading and Cleaning
```python
import numpy as np
import pandas as pd

# Load dataset
df = pd.read_csv("E commerce 2024.csv")

# Rename columns
df = df.rename(columns={'Price (Rs.)':'Price', 'Final_Price(Rs.)':'Final Price'})

# Drop irrelevant columns
df = df.drop('Product Id', axis=1)

# Handle missing values
df = df.dropna()
```

### Filtering and Sorting
```python
# Filter data
filtered_df = df[df['Final Price'] > 150]
filtered_df_loc = df.loc[df['Discount (%)'] < 35]
filtered_df_iloc = df.iloc[15:55]

# Sort data
Sorted_df = df.sort_values(by='Price', ascending=False)
```

### Aggregation
```python
# Aggregate data
agg_df = df.groupby('Final Price').agg('sum')
group_df = df.groupby('Category').agg({'Discount (%)':'sum', 'Price': 'mean'})
```

### Visualizations
#### Bar Plot for Total Sales by Category
```python
import matplotlib.pyplot as plt
category_sales = df.groupby('Category')['Final Price'].sum().reset_index()
plt.bar(category_sales['Category'], category_sales['Final Price'], color='skyblue')
plt.title('Total Sales by Category')
plt.xlabel('Category')
plt.ylabel('Total Sales (Rs.)')
plt.xticks(rotation=45)
plt.show()
```

#### Histogram for Discount Distribution
```python
import seaborn as sns
sns.histplot(df['Discount (%)'], bins=10, color='orange', kde=True)
plt.title('Discount Distribution')
plt.show()
```

#### Pie Chart for Payment Method Distribution
```python
payment_counts = df['Payment_Method'].value_counts()
plt.pie(payment_counts, labels=payment_counts.index, autopct='%1.1f%%', startangle=90, colors=sns.color_palette('pastel'))
plt.title('Payment Method Distribution')
plt.show()
```

#### Correlation Heatmap
```python
corr = df[['Price', 'Discount (%)', 'Final Price']].corr()
sns.heatmap(corr, annot=True, cmap='coolwarm', fmt='.2f', linewidths=0.5)
plt.title('Correlation Heatmap')
plt.show()
```

---

## Results
1. **Sales Insights**: Total sales by category are visualized through a bar chart.
2. **Discount Patterns**: The discount distribution is shown in a histogram, providing insights into discount ranges.
3. **Payment Preferences**: A pie chart represents the distribution of payment methods used.
4. **Correlations**: The heatmap highlights correlations between price, discount, and final price.

