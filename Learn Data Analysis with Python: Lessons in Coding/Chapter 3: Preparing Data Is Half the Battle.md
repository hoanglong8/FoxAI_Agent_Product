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

# Chapter 3: Preparing Data Is Half the Battle

## Listing 3-1: Method 1 - Standard Deviation
```python
import pandas as pd

Location = "datasets/gradedata.csv"

df = pd.read_csv(Location)

meangrade = df['grade'].mean()
stdgrade = df['grade'].std()

toprange = meangrade + stdgrade * 1.96
botrange = meangrade - stdgrade * 1.96

copydf = df
copydf = copydf.drop(copydf[copydf['grade'] > toprange].index)
copydf = copydf.drop(copydf[copydf['grade'] < botrange].index)

copydf
```
* Line 6: Calculate the upper boundary (1.96 * standard deviation + mean).
* Line 7: Calculate the lower boundary (mean - 1.96 * standard deviation).
* Line 9: Drop rows where grade is higher than toprange.
* Line 11: Drop rows where grade is lower than botrange.

## Listing 3-2: Method 2 - Interquartile Range (IQR)

```python
import pandas as pd

Location = "datasets/gradedata.csv"

df = pd.read_csv(Location)

q1 = df['grade'].quantile(.25)
q3 = df['grade'].quantile(.75)
iqr = q3 - q1

toprange = q3 + iqr * 1.5
botrange = q1 - iqr * 1.5

copydf = df
copydf = copydf.drop(copydf[copydf['grade'] > toprange].index)
copydf = copydf.drop(copydf[copydf['grade'] < botrange].index)

copydf
```

* Line 9: Compute upper boundary (Q3 + 1.5 * IQR).
* Line 10: Compute lower boundary (Q1 - 1.5 * IQR).
* Line 13: Drop rows where grade is higher than toprange.
* Line 14: Drop rows where grade is lower than botrange.

### Your Turn
Load the dataset datasets/outlierdata.csv. Can you remove the outliers?
Try using both methods (Standard Deviation & IQR).

### Listing 3-3: Creating Dataframe with Missing Data
```python
import pandas as pd

df = pd.read_csv("datasets/gradedatamissing.csv")

df.head()
```
This dataset contains missing data, which will be used to practice handling missing values.

