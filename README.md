# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
# ------------------------------------------
# 1. Import Required Libraries
# ------------------------------------------
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# ------------------------------------------
# 2. Read CSV File
# ------------------------------------------
df = pd.read_csv("SAMPLEIDS.csv")
print(df)
# ------------------------------------------
# 3. Dataset Information
# ------------------------------------------
a=df.info()
print(a)
# ------------------------------------------
# 4. Display Null Values
# ------------------------------------------
b=df.isnull()
print(b)

# ------------------------------------------
# 5. Display Null Count Column-wise
# ------------------------------------------
c=df.isnull().sum()
print(c)
# ------------------------------------------
# 6. Drop Rows Containing Null Values
# ------------------------------------------
df_dropna = df.dropna()
d=df_dropna.info()
print(d)
# ------------------------------------------
# 7. Fill Null with a Constant Value
# ------------------------------------------
df_constant = df.fillna(0)
e=df_constant.head()
print(e)
# ------------------------------------------
# 8. Fill Null using Forward Fill (ffill) or Backward Fill (bfill)
# ------------------------------------------
f=df_ffill = df.fillna(method='ffill')
g=df_bfill = df.fillna(method='bfill')
print(f)
print(g)
# ------------------------------------------
# 9. Calculate Mean of a Column and Fill Nulls
# (Example: replace 'age' with your column name)
# ------------------------------------------
mean_value = df['age'].mean()
h=df_mean = df.fillna({'age': mean_value})
print(h)
# ------------------------------------------
# 10. Drop All Null Values Completely
# ------------------------------------------
df_cleaned = df.dropna()
print(df_cleaned)
# ------------------------------------------
# 11. Boxplot to Detect Outliers
# ------------------------------------------
age = [1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af = pd.DataFrame(age, columns=['age'])

plt.boxplot(af['age'])
plt.title("Boxplot - Detect Outliers")
plt.show()

# ------------------------------------------
# 12. IQR Method to Find and Remove Outliers
# ------------------------------------------
Q1 = af['age'].quantile(0.25)
Q3 = af['age'].quantile(0.75)
IQR = Q3 - Q1

lower_limit = Q1 - 1.5 * IQR
upper_limit = Q3 + 1.5 * IQR

af_iqr_removed = af[(af['age'] >= lower_limit) & (af['age'] <= upper_limit)]

plt.boxplot(af_iqr_removed['age'])
plt.title("Boxplot After Removing Outliers (IQR Method)")
plt.show()

# ------------------------------------------
# 13. Z-Score Method to Detect & Remove Outliers
# ------------------------------------------
from scipy import stats

z_scores = np.abs(stats.zscore(af))
af_z_removed = af[(z_scores < 3).all(axis=1)]

plt.boxplot(af_z_removed['age'])
plt.title("Boxplot After Removing Outliers (Z-Score Method)")
plt.show()

# ------------------------------------------
# 14. Second Dataset for Outlier Analysis
# ------------------------------------------
from scipy import stats

data = [1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93,96,99,158]
df2 = pd.DataFrame(data, columns=['data'])

plt.boxplot(df2['data'])
plt.title("Initial Boxplot - Outlier Detection")
plt.show()

# --- IQR Method ---
Q1 = df2['data'].quantile(0.25)
Q3 = df2['data'].quantile(0.75)
IQR = Q3 - Q1

lower_limit = Q1 - 1.5 * IQR
upper_limit = Q3 + 1.5 * IQR

df2_iqr_removed = df2[(df2['data'] >= lower_limit) & (df2['data'] <= upper_limit)]

plt.boxplot(df2_iqr_removed['data'])
plt.title("Boxplot After IQR Outlier Removal")
plt.show()

# --- Z-Score Method ---
z_scores2 = np.abs(stats.zscore(df2))
df2_z_removed = df2[(z_scores2 < 3).all(axis=1)]

plt.boxplot(df2_z_removed['data'])
plt.title("Boxplot After Z-Score Outlier Removal")
plt.show()

```
![alt text](<Screenshot 2025-10-08 093623.png>)
![alt text](<Screenshot 2025-10-08 093643.png>)
![alt text](<Screenshot 2025-10-08 093654.png>)
![alt text](<Screenshot 2025-10-08 093701.png>)
![alt text](<Screenshot 2025-10-08 093714.png>)
![alt text](<Screenshot 2025-10-08 093728.png>)
![alt text](<Screenshot 2025-10-08 093741.png>)
![alt text](<Screenshot 2025-10-08 093753.png>)
![alt text](<Screenshot 2025-10-08 093800.png>)
![alt text](<Screenshot 2025-10-08 093808.png>)
![alt text](<Screenshot 2025-10-08 093814.png>)
![alt text](<Screenshot 2025-10-08 093819.png>)


# Result
    Hence the above program is excecuted successfully.
