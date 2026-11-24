# Experiment 2 : Customer Data Exploration Using Pandas

## Aim
To create a sample customer dataset and perform data exploration, filtering, sorting, grouping, and basic statistical analytics using Pandas functions in Python.

## Algorithm

1. **Start** the program.
2. **Import Library**: Import the `pandas` library as `pd` for tabular data manipulation and analysis.
3. **Initialize Dataset**: Create a Python dictionary `data` containing customer attributes (`Customer_ID`, `Customer_Name`, `Region`, `Age`, `Annual_Income`, `Spending_Score`, `Loyalty_Years`).
4. **Construct DataFrame**: Convert the dictionary into a structured Pandas DataFrame `df` using `pd.DataFrame(data)` and print the dataset.
5. **Inspect Structure & Summary**:
   * Display dataset dimensions (`df.shape`), column names (`df.columns`), data types and null counts (`df.info()`), and descriptive statistics (`df.describe()`).
   * Display the first 3 records (`df.head(3)`) and last 3 records (`df.tail(3)`).
6. **Sort & Filter Records**:
   * Sort customers in descending order of `Annual_Income` using `df.sort_values()`.
   * Filter high-income customers where `Annual_Income > 70000`.
7. **Perform Group-Wise & Frequency Analysis**:
   * Group customers by `Region` and calculate regional averages for `Annual_Income` and `Spending_Score` using `df.groupby().mean()`.
   * Count customer distribution across each region using `df["Region"].value_counts()`.
8. **Compute Overall Metrics & Top Performer**:
   * Identify the customer record with the highest `Spending_Score` using `df["Spending_Score"].idxmax()` and `df.loc[]`.
   * Calculate overall mean `Annual_Income` and mean `Spending_Score`.
9. **Stop** the program.

## Functions and Methods Used

| Category | Function / Method | Purpose / Description |
| :--- | :--- | :--- |
| **Data Creation** | `pd.DataFrame()` | Converts a Python dictionary into a 2D labeled tabular DataFrame |
| **Structural Inspection** | `df.shape`, `df.columns` | Retrieves dimensions `(rows, columns)` and column labels |
| | `df.info()`, `df.describe()` | Summarizes column data types, memory usage, and descriptive statistics |
| | `df.head(n)`, `df.tail(n)` | Views the first `n` and last `n` rows of the dataset |
| **Sorting & Filtering** | `df.sort_values()` | Orders records by `Annual_Income` in descending order |
| | Boolean Indexing (`df[...]`) | Filters customers with `Annual_Income > 70000` |
| **Grouping & Aggregation** | `df.groupby().mean()` | Aggregates mean income and spending score per `Region` |
| | `df["Region"].value_counts()` | Counts occurrences of customers in each region |
| | `idxmax()`, `df.loc[]`, `.mean()` | Locates the top spender row and computes dataset-wide averages |

## Program

#Customer Data Exploration using Pandas
```python
Step 1: Create a Sample Customer Dataset

import pandas as pd

data = {
    "Customer_ID": [101,102,103,104,105,106,107,108],
    "Customer_Name": ["Anita","Rajesh","Priya","Vikram","Divya","Manoj","Sita","Amit"],
    "Region": ["North","South","East","West","North","South","East","West"],
    "Age": [25,32,41,29,35,45,28,40],
    "Annual_Income": [55000,72000,61000,48000,85000,90000,64000,58000],
    "Spending_Score": [78,62,45,88,92,55,70,60],
    "Loyalty_Years": [2,5,4,3,6,7,3,4]
}

Step 2: Convert to a Pandas DataFrame

df = pd.DataFrame(data)

print("------CUSTOMER DATASET------")
print(df)

Step 3: Basic Exploration

print("\nShape of Dataset:", df.shape)
print("Columns:", df.columns.tolist())

print("\n-------Dataset Info-------")
df.info()

print("\n-----Summary Statistics-----")
print(df.describe())

Step 4: Display First and Last Few Records

print("\nFirst 3 Records:\n", df.head(3))
print("\nLast 3 Records:\n", df.tail(3))

Step 5: Sort Customers by Annual Income (Descending)

print("\nCustomers Sorted by Annual Income:\n",
      df.sort_values(by="Annual_Income", ascending=False))

Step 6: Filter High-Income Customers (Income greater than 70000)

print("\nHigh Income Customers (Income > 70000):\n",
      df[df["Annual_Income"] > 70000][["Customer_Name", "Annual_Income"]])

Step 7: Group Customers by Region and Find Average Income and Spending Score

print("\nRegion-wise Average Income and Spending Score:")
print(df.groupby("Region")[["Annual_Income", "Spending_Score"]].mean())

Step 8: Count Number of Customers in Each Region

print("\nCustomer Count per Region:")
print(df["Region"].value_counts())

Step 9: Identify Customer with Maximum Spending Score

top_customer = df["Spending_Score"].idxmax()

print("\nCustomer with Highest Spending Score:")
print(df.loc[top_customer])

Step 10: Compute Overall Averages

print("\nOverall Average Annual Income:",
      df["Annual_Income"].mean())

print("Overall Average Spending Score:",
      df["Spending_Score"].mean())
```

## Output
```text
------CUSTOMER DATASET------
   Customer_ID Customer_Name Region  Age  Annual_Income  Spending_Score  \
0          101         Anita  North   25          55000              78   
1          102        Rajesh  South   32          72000              62   
2          103         Priya   East   41          61000              45   
3          104        Vikram   West   29          48000              88   
4          105         Divya  North   35          85000              92   
5          106         Manoj  South   45          90000              55   
6          107          Sita   East   28          64000              70   
7          108          Amit   West   40          58000              60   

   Loyalty_Years  
0              2  
1              5  
2              4  
3              3  
4              6  
5              7  
6              3  
7              4  

Shape of Dataset: (8, 7)
Columns: ['Customer_ID', 'Customer_Name', 'Region', 'Age', 'Annual_Income', 'Spending_Score', 'Loyalty_Years']

-------Dataset Info-------
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 8 entries, 0 to 7
Data columns (total 7 columns):
 #   Column          Non-Null Count  Dtype 
---  ------          --------------  ----- 
 0   Customer_ID     8 non-null      int64 
 1   Customer_Name   8 non-null      object
 2   Region          8 non-null      object
 3   Age             8 non-null      int64 
 4   Annual_Income   8 non-null      int64 
 5   Spending_Score  8 non-null      int64 
 6   Loyalty_Years   8 non-null      int64 
dtypes: int64(5), object(2)
memory usage: 580.0+ bytes

-----Summary Statistics-----
       Customer_ID        Age  Annual_Income  Spending_Score  Loyalty_Years
count      8.00000   8.000000       8.000000        8.000000       8.000000
mean     104.50000  34.375000   66625.000000       68.750000       4.250000
std        2.44949   7.089983   14676.876857       16.359794       1.669046
min      101.00000  25.000000   48000.000000       45.000000       2.000000
25%      102.75000  28.750000   57250.000000       58.750000       3.000000
50%      104.50000  33.500000   62500.000000       66.000000       4.000000
75%      106.25000  40.250000   75250.000000       80.500000       5.250000
max      108.00000  45.000000   90000.000000       92.000000       7.000000

First 3 Records:
    Customer_ID Customer_Name Region  Age  Annual_Income  Spending_Score  \
0          101         Anita  North   25          55000              78   
1          102        Rajesh  South   32          72000              62   
2          103         Priya   East   41          61000              45   

   Loyalty_Years  
0              2  
1              5  
2              4  

Last 3 Records:
    Customer_ID Customer_Name Region  Age  Annual_Income  Spending_Score  \
5          106         Manoj  South   45          90000              55   
6          107          Sita   East   28          64000              70   
7          108          Amit   West   40          58000              60   

   Loyalty_Years  
5              7  
6              3  
7              4  

Customers Sorted by Annual Income:
    Customer_ID Customer_Name Region  Age  Annual_Income  Spending_Score  \
5          106         Manoj  South   45          90000              55   
4          105         Divya  North   35          85000              92   
1          102        Rajesh  South   32          72000              62   
6          107          Sita   East   28          64000              70   
2          103         Priya   East   41          61000              45   
7          108          Amit   West   40          58000              60   
0          101         Anita  North   25          55000              78   
3          104        Vikram   West   29          48000              88   

   Loyalty_Years  
5              7  
4              6  
1              5  
6              3  
2              4  
7              4  
0              2  
3              3  

High Income Customers (Income > 70000):
   Customer_Name  Annual_Income
1        Rajesh          72000
4         Divya          85000
5         Manoj          90000

Region-wise Average Income and Spending Score:
        Annual_Income  Spending_Score
Region                               
East          62500.0            57.5
North         70000.0            85.0
South         81000.0            58.5
West          53000.0            74.0

Customer Count per Region:
Region
North    2
South    2
East     2
West     2
Name: count, dtype: int64

Customer with Highest Spending Score:
Customer_ID         105
Customer_Name     Divya
Region            North
Age                  35
Annual_Income     85000
Spending_Score       92
Loyalty_Years         6
Name: 4, dtype: object

Overall Average Annual Income: 66625.0
Overall Average Spending Score: 68.75
```
## Result
The program successfully creates a customer dataset using Pandas and performs exploratory analysis, sorting, filtering, regional grouping, and summary statistics.
