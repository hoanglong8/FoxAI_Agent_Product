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
**Note:** This assumes that you have another dataframe already 
loaded into the df2 variable.

### Your Turn 
Can you export the dataframe created by the code shown in Listing 2-14 to Excel? 
Listing 2-14. Creating a Dataset for the Exercise 
```python
import pandas as pd 
names = ['Nike','Adidas','New Balance','Puma',’Reebok’] 
grades = [176,59,47,38,99] 
PriceList = zip(names,prices) 
df = pd.DataFrame(data = PriceList, columns=['Names',’Prices’])
```

### Combining Data from Multiple Excel Files
In earlier lessons, we opened single files and put their data into individual dataframes.
Sometimes, we need to combine the data from multiple Excel files into a single dataframe.

We can do this using two methods:
* Long way (manual appending for each file)
* Short way (automated file loading)

#### Long Way (Listing 2-15)
```python

import pandas as pd

all_data = pd.DataFrame()

df = pd.read_excel("datasets/data1.xlsx")
all_data = all_data.append(df, ignore_index=True)

df = pd.read_excel("datasets/data2.xlsx")
all_data = all_data.append(df, ignore_index=True)

df = pd.read_excel("datasets/data3.xlsx")
all_data = all_data.append(df, ignore_index=True)

all_data.describe()
```
This method does not scale well when handling hundreds of files, as it requires manual entry for each file.

#### Short Way (Listing 2-16)
```python

import pandas as pd
import glob

all_data = pd.DataFrame()

for f in glob.glob("datasets/data*.xlsx"):
    df = pd.read_excel(f)
    all_data = all_data.append(df, ignore_index=True)

all_data.describe()
```
This approach automatically loads all files matching a pattern (data*.xlsx) into a single dataframe.

### Your Turn
In the datasets/weekly_call_data folder, there are 104 files of weekly call data over two years.
Your task is to load all of that data into one dataframe.

## **Loading Data from SQL**
Normally, our data will come to us as **files** or **database links**.  
Let’s learn how to **load data from a SQLite database file** (**Listing 2-17**).

```python
import pandas as pd
from sqlalchemy import create_engine

# Connect to SQLite database
db_file = r'datasets/gradedata.db'
engine = create_engine(r"sqlite:///{}".format(db_file))

sql = 'SELECT * FROM test WHERE Grades IN (76,77,78)'

sales_data_df = pd.read_sql(sql, engine)
sales_data_df
This code creates a link to the gradedata.db database and executes a query to fetch relevant data.

If you don't know the names of the tables in a SQLite database,
use Listing 2-18 to find them:

python
Sao chép
Chỉnh sửa
sql = "SELECT name FROM sqlite_master WHERE type='table';"
Once you identify a table name, you can retrieve all its contents using Listing 2-19:

python
Sao chép
Chỉnh sửa
sql = "SELECT * FROM test;"
Now, running sales_data_df.head() will display the first few rows of the table.

For additional help, run Listing 2-20:

python
Sao chép
Chỉnh sửa
sales_data_df.read_sql?
Your Turn
Can you load data from the datasets/salesdata.db database?

Saving Data to SQL
To save a DataFrame to an SQL database, use Listing 2-21:

python
Sao chép
Chỉnh sửa
import pandas as pd

names = ['Bob', 'Jessica', 'Mary', 'John', 'Mel']
grades = [76, 95, 77, 78, 99]

GradeList = zip(names, grades)
df = pd.DataFrame(data=GradeList, columns=['Names', 'Grades'])

df
Now, let's export this DataFrame to a SQLite database (Listing 2-22):

python
Sao chép
Chỉnh sửa
import os
import sqlite3 as lite

db_filename = r'mydb.db'
con = lite.connect(db_filename)

df.to_sql('mytable', con, if_exists='replace')

con.close()
Line 14: mydb.db is the path and name of the SQLite database.
Line 18: 'mytable' is the name of the table created in the database.
For more details, check Listing 2-23:

python
Sao chép
Chỉnh sửa
df.to_sql?
Your Turn
Can you create a SQLite table containing data from datasets/gradedata.csv?

Random Numbers and Creating Random Data
In most cases, you will use these techniques on real datasets,
but sometimes you need to generate random data.

Let’s create a random list of baby names (Listing 2-24).

python
Sao chép
Chỉnh sửa
import pandas as pd
from numpy import random
from numpy.random import randint

names = ['Bob', 'Jessica', 'Mary', 'John', 'Mel']
First, we import necessary libraries and define a list of names.

Next, seed the random generator (Listing 2-25):

python
Sao chép
Chỉnh sửa
random.seed(500)
Why seed the random generator?
If you use the same seed, you will always get the same "random" numbers.

We will perform the following steps:

randint(low=0, high=len(names))

Generates a random integer between 0 and len(names)-1.
names[n]

Selects the name at index n.
for i in range(n)

Loops n times.
random_names = [...]

Selects random names n times.
Now, let's generate 1000 random names (Listing 2-26):

python
Sao chép
Chỉnh sửa
randnames = []

for i in range(1000):
    name = names[randint(low=0, high=len(names))]
    randnames.append(name)
We now have 1000 random names stored in randnames.

Now, let’s generate 1000 random numbers (Listing 2-27):

```python

births = []

for i in range(1000):
    births.append(randint(low=0, high=1000))
```
Finally, let's combine the two lists into a dataset (Listing 2-28):

```python

BabyDataSet2 = list(zip(randnames, births))

df = pd.DataFrame(data=BabyDataSet2, columns=['Names', 'Births'])

df
```
### Your Turn
Can you create a DataFrame called parkingtickets with 250 rows,
each containing a name and a random number between 1 and 25?
