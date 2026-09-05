# Exploratory Data Analysis (EDA) – Sample Superstore

## 1. Project Overview

This project performs **Exploratory Data Analysis (EDA)** on the **Sample Superstore dataset** using Python in Google Colab.

The analysis explores the structure of the dataset, statistical information, missing values, sales, profit, discount, delivery time, product categories, and correlations between numerical variables.

The project uses **Pandas, NumPy, Matplotlib, and Seaborn** for data analysis and visualization.

---

## 2. Objectives

The main objectives of this EDA project are:

* To understand the structure of the dataset.
* To inspect the rows and columns.
* To identify data types.
* To calculate statistical summaries.
* To convert date columns into proper datetime format.
* To calculate delivery days.
* To identify unique product categories.
* To check missing values.
* To analyze sales by category.
* To analyze sales distribution.
* To analyze profit by category.
* To study profit distribution.
* To analyze the effect of discount on profit.
* To identify correlations between numerical variables.
* To represent the findings using graphs.

---

## 3. Dataset


The dataset used is `samplesuperstore.csv`.

**Dataset:** Sample Superstore

The dataset contains information about customer orders, products, sales, quantity, discount, profit, order dates, shipping dates, and categories.

The dataset contains:

* **9128 rows**
* **21 columns**

Important columns include:

| Column      | Description                     |
| ----------- | ------------------------------- |
| Row ID      | Unique row identification       |
| Order ID    | Order identification            |
| Order Date  | Date when the order was placed  |
| Ship Date   | Date when the order was shipped |
| Ship Mode   | Shipping method                 |
| Customer ID | Customer identification         |
| Category    | Product category                |
| Sales       | Sales amount                    |
| Quantity    | Number of products              |
| Discount    | Discount percentage/value       |
| Profit      | Profit earned                   |

---

# 4. Technologies Used

### Programming Language

* Python

### Platform

* Google Colab

### Libraries

* **Pandas** – Data manipulation and analysis
* **NumPy** – Numerical operations
* **Matplotlib** – Data visualization
* **Seaborn** – Statistical visualization

---

# 5. EDA Implementation

## Step 1 – Import Libraries

### Code

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### Output

No output is produced because this cell only imports the required libraries.

---

## Step 2 – Load the Dataset

### Code

```python
df=pd.read_csv("/content/samplesuperstore.csv")
```

### Output

The dataset is successfully loaded into a Pandas DataFrame named `df`.

---

## Step 3 – Display First Five Records

### Code

```python
df.head()
```

### Output

The first five records of the dataset are displayed.

The output contains columns such as:

```text
Row ID
Order ID
Order Date
Ship Date
Ship Mode
Customer ID
...
```

The first records include order IDs such as:

```text
US-2023-103800
US-2023-112326
US-2023-141817
```

---

## Step 4 – Display Dataset Information

### Code

```python
df.info()
```

### Output

```text
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 9128 entries, 0 to 9127
Data columns (total 21 columns)
```

The dataset contains **9128 rows and 21 columns**.

Initially, the date columns are stored as `object` data types.

---

## Step 5 – Check Dataset Shape

### Code

```python
df.shape
```

### Output

```text
(9128, 21)
```

This means the dataset contains:

* Rows = **9128**
* Columns = **21**

---

## Step 6 – Statistical Description

### Code

```python
df.describe()
```

### Output

The `describe()` function provides statistical information about numerical columns such as:

* Row ID
* Sales
* Quantity
* Discount
* Profit

Some important values from the output are:

```text
Sales Mean       = 229.083092
Quantity Mean    = 3.786020
Discount Mean    = 0.155235
Profit Mean      = 29.361223
```

The minimum profit is approximately:

```text
-6599.978
```

This indicates that some transactions resulted in significant losses.

---

# 6. Data Preprocessing

## Step 7 – Convert Date Columns

### Code

```python
df['Order Date']=pd.to_datetime(df['Order Date'],format='mixed')
df['Ship Date']=pd.to_datetime(df['Ship Date'],format='mixed')
```

### Output

No direct output is produced.

The `Order Date` and `Ship Date` columns are converted from `object` to `datetime64[ns]`.

---

## Step 8 – Check Updated Data Types

### Code

```python
df.info()
```

### Output

The date columns are now displayed as:

```text
Order Date    datetime64[ns]
Ship Date     datetime64[ns]
```

This makes date-based calculations possible.

---

## Step 9 – Calculate Delivery Days

### Code

```python
df['Delivery Days']=(df['Ship Date']-df['Order Date']).dt.days
```

### Output

A new column called:

```text
Delivery Days
```

is added to the dataset.

It represents the number of days between the order date and shipping date.

---

## Step 10 – Display Updated Data

### Code

```python
df.head()
```

### Output

The first five rows are displayed with the converted dates and the newly calculated `Delivery Days` column.

---

# 7. Category Analysis

## Step 11 – Find Unique Categories

### Code

```python
df['Category'].unique()
```

### Output

```text
['Office Supplies', 'Furniture', 'Technology', nan]
```

The dataset contains three main product categories:

1. Office Supplies
2. Furniture
3. Technology

There is also one missing category value.

---

# 8. Missing Value Analysis

## Step 12 – Check Missing Values

### Code

```python
df.isnull().sum()
```

### Output

The analysis shows one missing value in several columns, including:

```text
Order ID           1
Order Date         1
Ship Date          1
Ship Mode          1
Customer ID        1
Customer Name      1
Segment            1
Category           1
Sales              1
Quantity           1
Discount           1
...
```

`Row ID` has no missing values.

This indicates that the dataset contains a small number of missing records that may require cleaning before further analysis.

---

# 9. Sales Analysis

## Step 13 – Calculate Sales by Category

### Code

```python
category_sales = (df.groupby('Category')['Sales'].sum())
category_sales
```

### Output

```text
Category
Furniture          678752.4825
Office Supplies    662959.4830
Technology         749129.4160
Name: Sales, dtype: float64
```

### Observation

Technology has the highest total sales among the three categories.

---

## Step 14 – Sales by Category Visualization

### Code

```python
category_sales.plot(kind='bar',figsize=(8,5))
plt.title("Sales by Category")
plt.ylabel("Total Sales")
plt.show()
```

### Output

A **bar chart** titled:

<img width="721" height="560" alt="image" src="https://github.com/user-attachments/assets/b3a689fc-0269-4b04-ad97-ef1e51ab36bf" />


```text
Sales by Category
```

is displayed.

The chart compares total sales for:

* Furniture
* Office Supplies
* Technology

---

# 10. Sales Distribution

## Step 15 – Sales Distribution Histogram

### Code

```python
plt.figure(figsize=(8,5))
sns.histplot(df['Sales'],bins=30)
plt.title("Sales Distribution")
plt.show()
```

### Output

A **histogram** titled:

<img width="704" height="470" alt="image" src="https://github.com/user-attachments/assets/4788e975-7312-4757-bc29-976a04b8c4f4" />


```text
Sales Distribution
```

is displayed.

The histogram shows how the sales values are distributed throughout the dataset.

---

# 11. Profit Analysis

## Step 16 – Profit by Category

### Code

```python
sns.barplot(
    data=df,
    x="Category",
    y="Profit"
)

plt.title("Profit by Category")
plt.show()
```

### Output

A bar chart titled:

<img width="571" height="455" alt="image" src="https://github.com/user-attachments/assets/e09a58a0-5bb8-4e2c-9375-6e5a7bfbfd66" />


```text
Profit by Category
```

is displayed.

It compares the profit values across different product categories.

---

## Step 17 – Profit Distribution

### Code

```python
sns.boxplot(
    data=df,
    y="Profit"
)

plt.title("Profit Distribution")
plt.show()
```

### Output

A **box plot** titled:

<img width="592" height="416" alt="image" src="https://github.com/user-attachments/assets/23965bb5-5bcc-4c61-a485-67a36cea942d" />


```text
Profit Distribution
```

is displayed.

The box plot helps identify:

* Median profit
* Spread of profit
* Outliers
* Negative profit values

---

## Step 18 – Profit Variation Across Categories

### Code

```python
sns.boxplot(
    data=df,
    x="Category",
    y="Profit"
)

plt.title("Profit Variation Across Categories")
plt.show()
```

### Output

A box plot titled:

<img width="592" height="455" alt="image" src="https://github.com/user-attachments/assets/409475b0-9a2a-428b-91c2-e1fc1313c332" />


```text
Profit Variation Across Categories
```

is displayed.

This visualization compares the distribution and variation of profit across categories.

---

# 12. Discount Analysis

## Step 19 – Display Unique Discount Values

### Code

```python
df["Discount"].unique()
```

### Output

```text
[0.2, 0.8, 0.0, 0.6, 0.15, 0.7,
 0.5, 0.4, 0.1, 0.3, 0.32, 0.45, nan]
```

This shows the different discount values present in the dataset.

---

## Step 20 – Impact of Discount on Profit

### Code

```python
sns.scatterplot(
    data=df,
    x="Discount",
    y="Profit"
)

plt.title("Impact of Discount on Profit")
plt.show()
```

### Output

A **scatter plot** titled:

<img width="592" height="455" alt="image" src="https://github.com/user-attachments/assets/31d43adb-fec5-412b-9f56-10921a5921a1" />


```text
Impact of Discount on Profit
```

is displayed.

The graph helps analyze the relationship between discount and profit.

---

# 13. Correlation Analysis

## Step 21 – Select Numerical Columns

### Code

```python
numeric_df = df.select_dtypes(
    include="number"
)
```

### Output

The numerical columns are selected for correlation analysis.

These include:

```text
Row ID
Sales
Quantity
Discount
Profit
Delivery Days
```

---

## Step 22 – Calculate Correlation

### Code

```python
corr = numeric_df.corr()
corr
```

### Output

Important correlation values include:

```text
Sales – Profit        = 0.492433
Sales – Quantity      = 0.203534
Discount – Profit     = -0.219258
Quantity – Profit     = 0.072212
```

### Observation

* Sales and Profit have a **positive correlation** of approximately `0.492`.
* Discount and Profit have a **negative correlation** of approximately `-0.219`.
* Sales and Quantity have a positive correlation of approximately `0.204`.

---

# 14. Correlation Heatmap

## Step 23 – Create Heatmap

### Code

```python
sns.heatmap(
    corr,
    annot=True
)

plt.title("Correlation Heatmap")
plt.show()
```

### Output

<img width="609" height="518" alt="image" src="https://github.com/user-attachments/assets/9f9c126e-0c81-409f-88ae-809906063f79" />


A **correlation heatmap** is displayed.

The heatmap visually represents the correlation between numerical variables.

---

# 15. Visualizations Included

The project contains the following visualizations:

1. **Sales by Category – Bar Chart**
2. **Sales Distribution – Histogram**
3. **Profit by Category – Bar Chart**
4. **Profit Distribution – Box Plot**
5. **Profit Variation Across Categories – Box Plot**
6. **Impact of Discount on Profit – Scatter Plot**
7. **Correlation Heatmap**

---

# 16. Key Findings

From the EDA:

* The dataset contains **9128 rows and 21 columns**.
* There are three main product categories: **Furniture, Office Supplies, and Technology**.
* **Technology** has the highest total sales with approximately **749,129.42**.
* Furniture has approximately **678,752.48** in total sales.
* Office Supplies has approximately **662,959.48** in total sales.
* The average sales value is approximately **229.08**.
* The average profit is approximately **29.36**.
* Some transactions have negative profit.
* There are missing values in several columns.
* Discount and profit show a negative correlation of approximately **-0.219**.
* Sales and profit show a positive correlation of approximately **0.492**.
* Delivery days were calculated using the order date and ship date.

---

# 17. Conclusion

The Exploratory Data Analysis of the Sample Superstore dataset provides an understanding of sales, profit, discount, product categories, and delivery time.

Using Python libraries such as Pandas, NumPy, Matplotlib, and Seaborn, the dataset was inspected, processed, analyzed, and visualized.

The analysis shows that **Technology has the highest total sales**, while the correlation analysis indicates a positive relationship between sales and profit and a negative relationship between discount and profit.

This EDA can be used as a foundation for further analysis, business intelligence, and predictive modeling.

---

# 18. Project Files

```text
EDA-Project/
│
├── EDA.ipynb
├── samplesuperstore.csv
└── README.md
```

## 19. How to Run

1. Open `EDA.ipynb` in **Google Colab**.
2. Upload `samplesuperstore.csv` to the Colab environment.
3. Run each cell sequentially.
4. The code will generate the displayed tables, statistical results, and visualizations.

### Required Libraries

```bash
pip install pandas numpy matplotlib seaborn
```
