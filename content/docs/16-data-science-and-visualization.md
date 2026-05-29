---
title: "Ch 16: Data Science & Visualization"
weight: 16
---

# Data Science & Visualization

## Learning Objectives

After reading this chapter, you will be able to:
- Use NumPy for numerical computing and array operations
- Use Pandas for data manipulation and analysis
- Create visualizations with Matplotlib and Seaborn
- Perform basic statistical analysis
- Understand the data science workflow
- Read and clean real-world datasets

---

## 16.1 NumPy Basics

```python
import numpy as np

# Creating arrays
arr1 = np.array([1, 2, 3, 4, 5])
arr2 = np.zeros((3, 4))           # 3x4 zeros
arr3 = np.ones((2, 3))            # 2x3 ones
arr4 = np.full((2, 2), 7)         # 2x2 all 7's
arr5 = np.eye(4)                  # 4x4 identity matrix
arr6 = np.random.randn(3, 3)      # 3x3 random normal
arr7 = np.arange(0, 10, 2)        # [0, 2, 4, 6, 8]
arr8 = np.linspace(0, 1, 5)      # [0, 0.25, 0.5, 0.75, 1]

# Array attributes
print(arr1.shape)    # (5,)
print(arr2.shape)    # (3, 4)
print(arr1.dtype)    # int64
print(arr1.ndim)     # 1
print(arr1.size)     # 5
```

### Array Operations

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(a + b)     # [5, 7, 9]
print(a - b)     # [-3, -3, -3]
print(a * b)     # [4, 10, 18]
print(a / b)     # [0.25, 0.4, 0.5]
print(a ** 2)    # [1, 4, 9]
print(np.sqrt(a))  # [1, 1.41, 1.73]
print(np.sum(a))   # 6
print(np.mean(a))  # 2.0
print(np.std(a))   # 0.816...

# Broadcasting
print(a + 10)     # [11, 12, 13]
print(a * [10])   # [10, 20, 30]

# Matrix operations
m1 = np.array([[1, 2], [3, 4]])
m2 = np.array([[5, 6], [7, 8]])
print(m1 @ m2)    # Matrix multiplication
print(m1.T)       # Transpose
print(np.linalg.inv(m1))  # Inverse
```

### Indexing and Slicing

```python
arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

print(arr[0, 1])      # 2
print(arr[:, 0])      # [1, 4, 7]
print(arr[0, :])      # [1, 2, 3]
print(arr[1:, 1:])    # [[5, 6], [8, 9]]

# Boolean indexing
print(arr[arr > 5])   # [6, 7, 8, 9]

# Fancy indexing
print(arr[[0, 2], [0, 2]])  # [1, 9]
```

---

## 16.2 Pandas Basics

```python
import pandas as pd

# Series (1D labeled array)
s = pd.Series([1, 3, 5, np.nan, 6, 8])
print(s)

s_with_index = pd.Series(
    [10, 20, 30],
    index=["a", "b", "c"]
)

# DataFrame (2D labeled table)
df = pd.DataFrame({
    "name": ["Alice", "Bob", "Charlie", "Diana"],
    "age": [25, 30, 35, 28],
    "salary": [50000, 60000, 70000, 55000],
    "department": ["Engineering", "Sales", "Engineering", "HR"]
})

print(df.head())  # First 5 rows
print(df.info())  # Column types, non-null counts
print(df.describe())  # Statistics summary
```

### Reading Data

```python
# CSV
df = pd.read_csv("data.csv")
df = pd.read_csv("data.csv", header=0, index_col=0)

# Excel
df = pd.read_excel("data.xlsx", sheet_name="Sheet1")

# JSON
df = pd.read_json("data.json")

# SQL
from sqlalchemy import create_engine
engine = create_engine("sqlite:///database.db")
df = pd.read_sql("SELECT * FROM users", engine)

# Parquet (efficient columnar storage)
df = pd.read_parquet("data.parquet")
```

### Data Exploration

```python
print(df.shape)      # (rows, columns)
print(df.columns)    # Column names
print(df.dtypes)     # Data types
print(df.head(10))   # First 10 rows
print(df.tail(5))    # Last 5 rows
print(df.sample(3))  # Random 3 rows

# Summary
print(df["age"].mean())
print(df["salary"].median())
print(df["department"].value_counts())
print(df.groupby("department")["salary"].mean())
```

### Selecting Data

```python
# Column selection
df["name"]           # Series
df[["name", "age"]]  # DataFrame
df.name              # Attribute access (if valid Python name)

# Row selection (by label)
df.loc[0]         # First row (by index label)
df.loc[0:2, ["name", "age"]]  # Rows 0-2, columns name and age

# Row selection (by position)
df.iloc[0]        # First row
df.iloc[1:3, 0:2] # Rows 1-2, columns 0-1

# Boolean indexing
df[df["age"] > 30]
df[(df["age"] > 25) & (df["department"] == "Engineering")]
df[df["name"].str.startswith("A")]

# Query
df.query("age > 30 and salary > 60000")
```

### Data Cleaning

```python
# Handle missing values
df.isnull().sum()  # Count nulls per column
df.dropna()        # Drop rows with nulls
df.fillna(0)       # Fill with 0
df.fillna(df.mean())  # Fill with column mean
df["age"].fillna(method="ffill")  # Forward fill

# Remove duplicates
df.duplicated().sum()  # Count duplicates
df.drop_duplicates()
df.drop_duplicates(subset=["email"])  # Based on column

# Rename columns
df.rename(columns={"old_name": "new_name"}, inplace=True)

# Change types
df["age"] = df["age"].astype(int)
df["date"] = pd.to_datetime(df["date"])

# Handle outliers
q1 = df["salary"].quantile(0.25)
q3 = df["salary"].quantile(0.75)
iqr = q3 - q1
df_clean = df[(df["salary"] >= q1 - 1.5*iqr) & (df["salary"] <= q3 + 1.5*iqr)]
```

### Grouping and Aggregation

```python
# Group by
summary = df.groupby("department")["salary"].agg(["mean", "median", "min", "max", "count"])

# Multiple aggregations
stats = df.groupby("department").agg({
    "salary": ["mean", "std"],
    "age": ["mean", "min", "max"],
    "name": "count"
})

# Pivot table
pivot = df.pivot_table(
    values="salary",
    index="department",
    columns="gender",
    aggfunc="mean"
)
```

### Merging and Joining

```python
# Concatenation
combined = pd.concat([df1, df2], axis=0)  # Stack rows
combined = pd.concat([df1, df2], axis=1)  # Stack columns

# SQL-like merges
inner = pd.merge(df1, df2, on="id", how="inner")  # Inner join
left = pd.merge(df1, df2, on="user_id", how="left")  # Left join
outer = pd.merge(df1, df2, on="id", how="outer")  # Full outer

# Join on index
df1.join(df2, how="left", lsuffix="_left", rsuffix="_right")
```

---

## 16.3 Matplotlib

```python
import matplotlib.pyplot as plt

# Line plot
x = [1, 2, 3, 4, 5]
y = [1, 4, 9, 16, 25]

plt.figure(figsize=(10, 6))
plt.plot(x, y, "b-", label="x²", linewidth=2)
plt.plot(x, [xi**3 for xi in x], "r--", label="x³")
plt.xlabel("X values")
plt.ylabel("Y values")
plt.title("Simple Plot")
plt.legend()
plt.grid(True, alpha=0.3)
plt.savefig("plot.png", dpi=300, bbox_inches="tight")
plt.show()

# Bar chart
categories = ["A", "B", "C", "D"]
values = [23, 45, 56, 78]
plt.bar(categories, values, color="skyblue", edgecolor="navy")
plt.title("Bar Chart")
plt.show()

# Histogram
data = np.random.randn(1000)
plt.hist(data, bins=30, alpha=0.7, edgecolor="black")
plt.title("Histogram")
plt.show()

# Scatter plot
x = np.random.randn(100)
y = x + np.random.randn(100) * 0.5
plt.scatter(x, y, alpha=0.6, c=x, cmap="viridis")
plt.colorbar(label="Color scale")
plt.title("Scatter Plot")
plt.show()

# Subplots
fig, axes = plt.subplots(2, 2, figsize=(12, 8))
axes[0, 0].plot(x, y)
axes[0, 1].scatter(x, y)
axes[1, 0].hist(data, bins=20)
axes[1, 1].bar(categories, values)
plt.tight_layout()
plt.show()
```

---

## 16.4 Seaborn

```python
import seaborn as sns

# Load built-in dataset
tips = sns.load_dataset("tips")
print(tips.head())

# Style
sns.set_theme(style="whitegrid")

# Distribution plot
sns.histplot(data=tips, x="total_bill", bins=30, kde=True)
sns.kdeplot(data=tips, x="total_bill", hue="time", fill=True)

# Box plot
sns.boxplot(data=tips, x="day", y="total_bill", hue="sex")

# Violin plot
sns.violinplot(data=tips, x="day", y="total_bill")

# Correlation heatmap
corr = tips.corr(numeric_only=True)
sns.heatmap(corr, annot=True, cmap="coolwarm", center=0)

# Pair plot (scatter matrix)
sns.pairplot(tips, hue="sex", diag_kind="kde")

# Count plot
sns.countplot(data=tips, x="day", hue="smoker")

# Regression plot
sns.regplot(data=tips, x="total_bill", y="tip")

# Facet grid
sns.lmplot(data=tips, x="total_bill", y="tip", col="day", hue="sex")

plt.show()
```

---

## Key Takeaways

- **NumPy** provides fast array operations and linear algebra
- **Pandas** is essential for data manipulation (filter, group, merge, clean)
- **Matplotlib** is the foundational plotting library
- **Seaborn** provides high-level statistical visualizations
- The data science workflow: Load → Clean → Explore → Model → Communicate
- Use `groupby()` and `pivot_table()` for data aggregation
- Always check for missing values and outliers early
- Visualizations reveal patterns that summary statistics miss

---

## Exercises

1. **NumPy**: Create a 5x5 matrix with 1s on the border and 0s inside
2. **Pandas**: Load a CSV, find missing values, fill them, and compute group summaries
3. **Data cleaning**: Clean a messy dataset — handle duplicates, outliers, missing data
4. **Matplotlib**: Create a multi-panel figure with line, bar, scatter, and histogram
5. **Seaborn**: Explore the `tips` or `iris` dataset with pairplot and heatmap
6. **Analysis**: Find correlation between columns in a real dataset and visualize

---

## Next Steps

→ Continue to [Chapter 17: Interview Questions & Answers]({{< relref "17-interview-questions-and-answers" >}})
