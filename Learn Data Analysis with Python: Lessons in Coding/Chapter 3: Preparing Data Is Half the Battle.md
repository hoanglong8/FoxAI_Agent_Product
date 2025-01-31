# Chapter 3: Preparing Data Is Half the Battle

The second step of data analysis is **cleaning the data**.  
Getting data ready for analytical tools can be a **difficult task**.  
Python and its libraries try to make it **as easy as possible**.

With just a few lines of code, you will be able to:
- **Clean the data**
- **Create new variables**
- **Organize the data**

---

## **Cleaning Data**

To be useful for most analytical tasks, data must be:
- **Consistent**
- **Relevant**
- **Standardized**

In this chapter, you will learn how to:
- **Remove outliers**
- **Handle missing data**
- **Filter inappropriate values**
- **Find duplicate rows**
- **Remove punctuation**
- **Remove whitespace**
- **Standardize dates**
- **Standardize text**

---

## **Calculating and Removing Outliers**

Imagine collecting **income data** from your high school classmates.  
If **Bill Gates** was one of them, the average **net worth** of your class would be **skewed**.

Outliers can be detected using **two methods**:

1. **Standard Deviations**  
   - 95% of data is within **1.96 standard deviations** of the mean.  
   - Any values **beyond this range** can be **removed**.

2. **Interquartile Range (IQR)**  
   - IQR = **Q3 - Q1**  
   - Outliers are values **below** `Q1 - 1.5 * IQR` or **above** `Q3 + 1.5 * IQR`.  

Let's see these methods in action.

### Method 1: Standard Deviation
```python
import pandas as pd

Location = "datasets/gradedata.csv"
df = pd.read_csv(Location)

meangrade = df['grade'].mean()
stdgrade = df['grade'].std()

toprange = meangrade + stdgrade * 1.96
botrange = meangrade - stdgrade * 1.96

df = df.drop(df[df['grade'] > toprange].index)
df = df.drop(df[df['grade'] < botrange].index)

df
```
### Method 2: Interquartile Range
```python

import pandas as pd

Location = "datasets/gradedata.csv"
df = pd.read_csv(Location)

q1 = df['grade'].quantile(0.25)
q3 = df['grade'].quantile(0.75)
iqr = q3 - q1

toprange = q3 + iqr * 1.5
botrange = q1 - iqr * 1.5

df = df.drop(df[df['grade'] > toprange].index)
df = df.drop(df[df['grade'] < botrange].index)

df
```
### Your Turn
Can you remove outliers from datasets/test_scores.csv using both methods?

## Missing Data in Pandas DataFrames
Sometimes datasets contain missing values that need to be handled.

### Method 1: Drop Missing Values
```python

df = df.dropna()
```
### Method 2: Fill Missing Values with a Default
```python

df = df.fillna(0)
```
### Method 3: Fill Missing Values with the Column Mean
```python

df['grade'] = df['grade'].fillna(df['grade'].mean())
```
### Filtering Inappropriate Values
Some values in datasets don’t make sense (e.g., grades over 100).
We can filter them out.

#### Create a DataFrame with Invalid Grades
```python

import pandas as pd

names = ['Bob', 'Jessica', 'Mary', 'John', 'Mel']
grades = [76, -2, 77, 78, 101]

df = pd.DataFrame(list(zip(names, grades)), columns=['Names', 'Grades'])
df
```
#### Filter Out Impossible Grades
```python

df = df[df['Grades'] <= 100]
```
#### Replace Out-of-Range Values with Max/Min

```python

df.loc[df['Grades'] > 100, 'Grades'] = 100
df.loc[df['Grades'] < 0, 'Grades'] = 0
```
### Finding Duplicate Rows
Duplicate rows can exist in datasets and should be handled properly.

#### Create a DataFrame with Duplicates
```python
 as pd

names = ['Jan', 'John', 'Bob', 'Jan', 'Mary', 'Jon', 'Mel', 'Mel']
grades = [95, 78, 76, 95, 77, 78, 99, 100]

df = pd.DataFrame(list(zip(names, grades)), columns=['Names', 'Grades'])
df
```
#### Detect Duplicates
```python

df.duplicated()
```
#### Remove Duplicates
```python

df = df.drop_duplicates()
```
### Your Turn
Can you load datasets/dupedata.csv and remove duplicate addresses?

### Removing Punctuation from Column Contents
Punctuation sometimes appears in text columns and needs to be removed.

Example: Cleaning Address Data
```python

import string

def remove_punctuation(text):
    return ''.join(char for char in text if char not in string.punctuation)

df['address'] = df['address'].apply(remove_punctuation)
```
#### Removing Whitespace from Column Contents
Whitespace can cause errors when analyzing text data.

```python

df['address'] = df['address'].str.strip()
```
#### Standardizing Dates
Different sources format dates differently (01/03/80, 1980/01/03, etc.). We can standardize them.

Example: Standardizing Birthdates
```python

from datetime import datetime

def standardize_date(date):
    return datetime.strptime(date, '%m/%d/%Y').strftime('%Y-%m-%d')

df['birthdate'] = df['birthdate'].apply(standardize_date)
```
### Your Turn
Can you convert datasets/employees.csv birthdates into YYYY-MM-DD format?
