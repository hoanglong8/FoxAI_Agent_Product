# Chapter 2: Getting Data Into and Out of Python

The first stage of data analysis is getting the data.  
Moving your data from where it is stored into your analytical tools and back out again can be a challenging task if you don’t know what you’re doing.  
Python and its libraries try to make this as easy as possible.

With just a few lines of code, you will be able to **import and export data** in the following formats:
- **CSV**
- **Excel**
- **SQL**

---

## **Loading Data from CSV Files**
Normally, data will come to us as **files** or **database links**.  
See **Listing 2-1** to learn how to load data from a CSV file.

```python
import pandas as pd

Location = "datasets/smallgradesh.csv"

df = pd.read_csv(Location, header=None)
```
Now, let’s take a look at what our data looks like (Listing 2-2):

```python

df.head()
```
As you can see, our dataframe lacks column headers.
To load data that includes headers, use the code in Listing 2-3:

```python

import pandas as pd

Location = "datasets/gradedata.csv"

df = pd.read_csv(Location)
```
Again, let’s display the first five rows (Listing 2-4):

```python

df.head()
```
If your dataset does not include headers, you can add them afterward using Listing 2-5.

```python

import pandas as pd

Location = "datasets/smallgrades.csv"
```

Add headers while loading the data
```python
df = pd.read_csv(Location, names=['Names', 'Grades'])
```

Add headers to an existing dataframe
```python
df.columns = ['Names', 'Grades']
```

### Your Turn
Can you create a dataframe from a file you uploaded and imported on your own?
Try this:

Visit http://census.ire.org/data/bulkdata.html.
Download a CSV data file for any state.
Import the data into Python.
Saving Data to CSV

If you want to save your progress while analyzing data or prepare data for another tool, exporting to CSV is useful.
See Listing 2-6 for an example.

```python

import pandas as pd

names = ['Bob', 'Jessica', 'Mary', 'John', 'Mel']
grades = [76, 95, 77, 78, 99]

GradeList = zip(names, grades)

df = pd.DataFrame(data=GradeList, columns=['Names', 'Grades'])

df.to_csv('studentgrades.csv', index=False, header=False)
```
The only parameters we use are:

index and header: Setting these parameters to False prevents the index and headers from being exported.
Try changing these values to understand their effects.

### Your Turn
Can you export the dataframe created by Listing 2-8 to a CSV file?

```python

import pandas as pd

names = ['Bob', 'Jessica', 'Mary', 'John', 'Mel']
grades = [76, 95, 77, 78, 99]
bsdegrees = [1, 1, 0, 0, 1]
msdegrees = [2, 1, 0, 0, 0]
phddegrees = [0, 1, 0, 0, 0]

Degrees = zip(names, grades, bsdegrees, msdegrees, phddegrees)
columns = ['Names', 'Grades', 'BS', 'MS', 'PhD']

df = pd.DataFrame(data=Degrees, columns=columns)

df
```
Loading Data from Excel Files
Normally, data will come to us as files or database links.
Let’s see how to load data from an Excel file (Listing 2-9).

```python

import pandas as pd

Location = "datasets/gradedata.xlsx"

df = pd.read_excel(Location)
```
Again, let’s take a look at the first five rows (Listing 2-10):

```python

df.head()
```
If you wish to change or simplify your column names, run Listing 2-11:

```python

df.columns = ['first', 'last', 'sex', 'age', 'exer', 'hrs', 'grd', 'addr']

df.head()
```

### Your Turn
Can you create a dataframe from a file you uploaded and imported on your own?

Visit https://www.census.gov/support/USACdataDownloads.html.
Download an Excel data file.
Import the data into Python.
Saving Data to Excel Files
To save a dataframe to an Excel file, use the code in Listing 2-12.

```python
import pandas as pd

names = ['Bob', 'Jessica', 'Mary', 'John', 'Mel']
grades = [76, 95, 77, 78, 99]

GradeList = zip(names, grades)

df = pd.DataFrame(data=GradeList, columns=['Names', 'Grades'])

writer = pd.ExcelWriter('dataframe.xlsx', engine='xlsxwriter')

df.to_excel(writer, sheet_name='Sheet1')

writer.save()
```
If you wish to save multiple dataframes to different sheets, use Listing 2-13:

```python
writer = pd.ExcelWriter('dataframe.xlsx', engine='xlsxwriter')

df.to_excel(writer, sheet_name='Sheet1')

df2.to_excel(writer, sheet_name='Sheet2')

writer.save()
```
