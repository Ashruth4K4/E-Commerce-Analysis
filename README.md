
# UK-Based Online Retail Transactions Dataset Analysis

## Overview

This repository contains an analysis of a transactional dataset from a UK-based non-store online retail company. The dataset includes all transactions from **01/12/2010** to **09/12/2011**. The company specializes in selling unique all-occasion gifts, with many customers being wholesalers. This analysis aims to provide insights into sales trends, top products, customer behavior, and country-based sales distributions.

## Dataset

- **Time period**: 01/12/2010 to 09/12/2011
- **Region**: Primarily UK-based transactions
- **Business type**: Non-store online retail
- **Customers**: Includes both individual customers and wholesalers
- **Main Products**: Unique all-occasion gifts

### Key Columns:
- **InvoiceNo**: Unique identifier for transactions
- **StockCode**: Product code
- **Description**: Product description
- **Quantity**: Number of products purchased
- **InvoiceDate**: Date and time of transaction
- **UnitPrice**: Price of each product
- **CustomerID**: Unique identifier for customers
- **Country**: Country of the customer

## Objectives

The main objectives of this project are:
1. **Data Cleaning and Preprocessing**:
   - Handle missing values in product descriptions and customer IDs.
   - Convert date columns into appropriate datetime formats for easier analysis.
   
2. **Exploratory Data Analysis (EDA)**:
   - Analyze sales trends over time, especially on a yearly basis.
   - Identify the top-selling products and countries contributing the most to sales.
   - Investigate customer spending behavior and country-wise customer distribution.
   
3. **Visualization**:
   - Generate plots and charts for insights into product popularity, revenue generation, and sales trends.

## Tools and Libraries Used

- **Pandas**: For data manipulation and preprocessing.
- **NumPy**: To perform numerical operations.
- **Matplotlib** & **Seaborn**: For data visualization.
- **Jupyter Notebook**: For interactive analysis.

## Key Code Segments

### 1. Data Preprocessing
The dataset is loaded and cleaned by filling missing values and converting the `InvoiceDate` column to a datetime format.
```python
df = pd.read_csv('e-commerce.csv', encoding='ISO-8859-1')
df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate'], format='%m/%d/%Y %H:%M')
df['Description'].fillna('Unknown', inplace=True)
df['CustomerID'].fillna(-1, inplace=True)
```

### 2. Yearly Sales Trends
We grouped data by year and visualized sales trends.
```python
df['Year'] = df['InvoiceDate'].dt.to_period('Y')
yearly_sales = df.groupby('Year')['Quantity'].sum()
```

### 3. Country-Wise Sales
We calculated total quantity sold by each country and highlighted the top 5 countries.
```python
country_sales = df.groupby('Country')['Quantity'].sum()
top_5_countries = country_sales.sort_values(ascending=False).head(5)
```

### 4. Top-Selling Products
We identified the top 10 best-selling products by quantity sold.
```python
top_products = df.groupby('Description')['Quantity'].sum().sort_values(ascending=False).head(10)
```

### 5. Visualizing Data
Several visualizations were created, including sales trends, top-selling products, top countries by customer count, and revenue-generating products.
```python
# Sales Trends Over Time
plt.figure(figsize=(12, 6))
plt.plot(monthly_sales.index.astype(str), monthly_sales.values, marker='o')
plt.title('Yearly Sales Trends')

# Pie Chart of Top 10 Products by Revenue
plt.figure(figsize=(8,8))
plt.pie(top_revenue_products.values, labels=top_revenue_products.index, autopct='%1.1f%%')
plt.title('Top 10 Products by Revenue')
plt.show()
```

## Visualizations

- **Yearly Sales Trends**: Shows the total quantity sold for each year.
- **Top 10 Best-Selling Products**: Bar chart of the top-selling products by quantity.
- **Top 10 Countries by Customer Count**: Bar chart of the countries with the most unique customers.
- **Top Products by Revenue**: Pie chart showcasing products contributing the most to revenue.

## How to Run the Code

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/online-retail-analysis.git
   ```
2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the Jupyter notebook:
   ```bash
   jupyter notebook retail_analysis.ipynb
   ```

## License

This project is licensed under the MIT License.

---

Feel free to modify the "How to Run the Code" section if the execution method changes or add more insights based on further analysis.
