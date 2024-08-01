# DATA ANALYSIS
This blog is just to give a bried summary on Data Analysis. 
Its a course i've been taking under IBM,and i'll give or highlight some of the things that i learned from this course.
#### In this,we are going to cover the following
### How to import data 
### Data pre-processing 
### Data formatting 
### Descriptive statistics

## How to import Data/Importing Data
Importing Data is the process of loading and reading data into python from various resources.

#### Two impportant properties to consider are:
### Format -> This tells the format in which the file is in eg csv, json.
### File path of dataset -> This tells us where the data is stored

## Steps of importing a data set 
```.py
import pandas as pd
url = "give the url"
#use pandas to convert the data into dataframe and store it in avariable df
df = pd.read.csv(url,header = none) #where there no titles for the header
df   #prints the entire dataframe
df.head(n)  #prints the first n rows of the dataframe
df.tail(n)  #prints the last/bottom n rows of the dataframe
```
## Adding headers
Using the above code the dataframe that will be printed will have no headers and the headers will be inoitialized using intergers ie 0,1,2...In orde rto curb that we use the following code and function
```.py
headers = ["a list of headers from another file online"]
df.columns = headers
```
## Exporting a pandas dataframe to csv
Preserve your progress anytime by saving modified dataset using the following function
```.py
path = "a path where you want to write your file with the file name"
#For example, if you save the data frame df as automobile.csv to your local machine, you may use the syntax below, where index = False means the row names will not be written.
# eg df.to_csv("automobile.csv", index=False)
df.to_csv(path)
```

You can also read and save other file formats. You can use similar functions like **`pd.read_csv()`** and **`df.to_csv()`** for other data formats. The functions are listed in the following table:

<h3>Read/Save Other Data Formats</h3>

| Data Formate |        Read       |            Save |
| ------------ | :---------------: | --------------: |
| csv          |  `pd.read_csv()`  |   `df.to_csv()` |
| json         |  `pd.read_json()` |  `df.to_json()` |
| excel        | `pd.read_excel()` | `df.to_excel()` |
| hdf          |  `pd.read_hdf()`  |   `df.to_hdf()` |
| sql          |  `pd.read_sql()`  |   `df.to_sql()` |
| ...          |        ...        |             ... |


<h2> Basic Insights from the Data set </h2>

<p>
  In pandas we use different funxtions in order to gain or get some insights from the dataframe<br>
  The following the functions used to to gain the insights<br>
  In thsi case we are using <b>df</b> to represent the name of our dataset<br>

  **`df.dtypes()`** -> is used to check datatypes,this helps in getting the overview datatype and rectifying the once with an error<br>
  
  **`df.describe()`** -> is used to return a statistical summary of the dataframe  where the data tpyes are exclusively numerical ie float,int... <br>
  
  **`df.describe(include ="all")`** -> is used to to return a statistical summary of the dataframe including the data with the object datatype<br>
  
  **`df.info()`** -> is used to provide a concide summary of your dataframe
</p>





