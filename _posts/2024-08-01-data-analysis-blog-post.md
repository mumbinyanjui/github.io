# DATA ANALYSIS
This blog is just to give a brief summary on Data Analysis. 
Its a course i've been taking under IBM,and i'll give or highlight some of the things that i learned from this course.
#### In this,we are going to cover the following
### How to import data 
### Data pre-processing 
### Data visualization 
### Report on the data insights

## How to import Data/Importing Data
Importing Data is the process of loading and reading data into python from various resources.

#### Two impportant properties to consider are:
### Format -> This tells the format in which the file is in eg csv, json.
### File path of dataset -> This tells us where the data is stored

## Steps of importing a data set 
```.py
import pandas as pd
#url = "give the url"
url = "C:\Users\ADMIN\Downloads\Student_performance_data _.csv"
#use pandas to convert the data into dataframe and store it in avariable df
#df = pd.read.csv(url,header = none) #where there no titles for the header
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
  In pandas we use different functions in order to gain or get some insights from the dataframe<br>
  The following the functions used to to gain the insights<br>
  In thsi case we are using <b>df</b> to represent the name of our dataset<br>

  **`df.dtypes()`** -> is used to check datatypes,this helps in getting the overview datatype and rectifying the once with an error<br>
  
  **`df.describe()`** -> is used to return a statistical summary of the dataframe  where the data tpyes are exclusively numerical ie float,int... <br>
  
  **`df.describe(include ="all")`** -> is used to to return a statistical summary of the dataframe including the data with the object datatype<br>
  
  **`df.info()`** -> is used to provide a concide summary of your dataframe
</p>

<h2>DATA PRE-PROCESSING</h2> 
<p>
 Data pre-processng involves:<br>
  . <i>Data cleaning</i> <br>
  . <i>Normalization of the data</i><br>
  . <i>Dummy variables</i>
</p>

<h3>1.Data cleanimg</h3>
<h4>1.1 Find missing values</h4>
<p>In finding missing values we use the following functions<br>
You can use the isnull() method combined with sum() to see if there are any missing values in the dataset.
</p>

```.py
#Sample DataFrame with missing values
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
    'Age': [25, None, 30, None, 22],
    'Gender': ['F', 'M', None, 'M', 'F'],
    'Score': [85, 90, None, 75, 95]
    }
    df = pd.DataFrame(data)

#Check for missing values in the entire DataFrame
print("Missing Values in Each Column:")
print(df.isnull().sum())

#Check for missing values in a specific column
print("\nMissing Values in 'Age' Column:")
print(df['Age'].isnull().sum())

#Display rows with missing values
print("\nRows with Missing Values:")
print(df[df.isnull().any(axis=1)])

#Check if any missing values are present
print("\nAny Missing Values in the DataFrame?")
print(df.isnull().values.any())

```
<h4>1.2 Dropping Missing Values</h4>
<p>Dropping missing values can be a straightforward solution, but it should be used with caution, especially if the missing data is a significant portion of the dataset. Pandas provides functions to drop missing values in various ways.<br>

1.2.1 Dropping Rows with Missing Values<br>
You can drop rows with missing values using dropna().
</p>

```.py
#Drop rows with any missing values
df_dropped_rows_any = df.dropna()
print("DataFrame after Dropping Rows with Any Missing Values:")
print(df_dropped_rows_any)

# Drop rows with missing values in a specific column
df_dropped_rows_specific = df.dropna(subset=['Age'])
print("\nDataFrame after Dropping Rows with Missing 'Age':")
print(df_dropped_rows_specific)
```
<p>1.2.2 Dropping Columns with Missing Values
You can also drop entire columns if they contain missing values, which is often used when a column has too many missing values and is deemed unnecessary.</p>

```.py
# Drop columns with any missing values
df_dropped_columns = df.dropna(axis=1)
print("DataFrame after Dropping Columns with Any Missing Values:")
print(df_dropped_columns)
```

<h4> 1.3 Replacing Missing Values:</h4>
Instead of dropping missing values, you can replace them with meaningful values such as the mean, median, mode, or a specific value. This is often preferred to retain as much data as possible.

1.3.1 Replacing with a Specific Value
```.py
# Replace missing values with a specific value (e.g., 0)
df_replaced_specific = df.fillna(0)
print("DataFrame after Replacing Missing Values with 0:")
print(df_replaced_specific)
```
<p>1.3.2. Replacing with Mean, Median, or Mode:
Replacing missing values with statistical measures like mean, median, or mode is common for numerical data.</p>

```.py
# Replace missing values with the mean of the column
df_replaced_mean = df.copy()
df_replaced_mean['Age'].fillna(df['Age'].mean(), inplace=True)
df_replaced_mean['Score'].fillna(df['Score'].mean(), inplace=True)
print("DataFrame after Replacing Missing Values with Mean:")
print(df_replaced_mean)

# Replace missing values with the median of the column
df_replaced_median = df.copy()
df_replaced_median['Age'].fillna(df['Age'].median(), inplace=True)
df_replaced_median['Score'].fillna(df['Score'].median(), inplace=True)
print("\nDataFrame after Replacing Missing Values with Median:")
print(df_replaced_median)

# Replace missing values with the mode of the column
df_replaced_mode = df.copy()
df_replaced_mode['Gender'].fillna(df['Gender'].mode()[0], inplace=True)
print("\nDataFrame after Replacing Missing Values with Mode:")
print(df_replaced_mode)
```

<h4>1.3 Drop Unnecessary Columns:</h4>

If there are columns that aren't needed for your analysis, you can drop them.

```.py
df.drop(columns=['UnnecessaryColumn1', 'UnnecessaryColumn2'], inplace=True)
```
<h4>1.4 Rename Columns:</h4>

Sometimes, column names might not be descriptive. You can rename them using the rename() method.
```.py
df.rename(columns={'OldName1': 'NewName1', 'OldName2': 'NewName2'}, inplace=True)
```
<h4>1.5 Check Data Types:</h4>

Ensure that the data types of each column are correct. You can convert them if necessary.

```.py
print(df.dtypes)

# Convert data types
df['NumericColumn'] = df['NumericColumn'].astype(float)
df['CategoricalColumn'] = df['CategoricalColumn'].astype('category')
```
<h4>1.6 Remove Duplicates: </h4>

Check and remove any duplicate rows if present.

```.py
df.drop_duplicates(inplace=True)
```
<h4>1.7 Reset Index:</h4>

After cleaning, it's often a good idea to reset the DataFrame's index.
```.py
df.reset_index(drop=True, inplace=True)
```

<h3>Normalization of data</h3>
<p>Normalization is a key data preprocessing technique used to transform features into a similar scale or range. This process ensures that the features have a consistent scale, making it easier to train machine learning models, especially those sensitive to the scale of input features, like gradient descent-based algorithms (e.g., linear regression, neural networks).<br>

Normalization can also help improve the convergence speed of optimization algorithms and the interpretability of models. It’s crucial when different features have varying units or scales, such as when mixing height (in centimeters) and weight (in kilograms).<br>

Here's a detailed explanation of normalization, its importance, and various methods to implement it in Python with examples and outputs.</p>>

<h4>Importance of Normalization</h4>
<p>
<i>1. Improved Model Convergence:</i> Algorithms like gradient descent converge faster when the input features are on a similar scale. Normalization helps in achieving this consistency.<br>
<i>2. Enhanced Model Performance:</i> Models like K-Nearest Neighbors (KNN) and Support Vector Machines (SVM) are sensitive to the scale of data. Normalization can improve their performance.<br>
<i>3. Better Interpretability:</i> Normalized features can make it easier to interpret the importance of features in a model, especially in linear models.</p>
<h4>Common Methods of Normalization</h4>
<p>
  <i>
1. Min-Max Normalization (Rescaling)<br>
2. Z-Score Normalization (Standardization)<br>
3. MaxAbs Scaling<br>
4. Robust Scaling<br>
5. Decimal Scaling<br>
6. L1 and L2 Normalization<br>
</i>
</p>
Let's explore the first two  methods with Python examples using the pandas and scikit-learn libraries,since they are the widely commonly used methods.
<h3>1. Min-Max Normalization (Rescaling)</h3>
<p>
Min-Max Normalization scales the data to a fixed range, typically [0, 1]. The formula for Min-Max Normalization is:<br>

𝑋′=𝑋−𝑋min/𝑋max−𝑋min<br>
Where:𝑋′  is the normalized value.<br>
      X is the original value.<br>
      Xmin and Xmax  are the minimum and maximum values of the feature, respectively.<br>
      </p>
#### Example
```.py
import pandas as pd
from sklearn.preprocessing import MinMaxScaler

# Sample data
data = {
    'Height': [150, 160, 170, 180, 190],
    'Weight': [50, 60, 70, 80, 90],
    'Age': [25, 35, 45, 55, 65]
}

df = pd.DataFrame(data)

# Initialize Min-Max Scaler
scaler = MinMaxScaler()

# Apply Min-Max Normalization
df_minmax = pd.DataFrame(scaler.fit_transform(df), columns=df.columns)

print("Original Data:")
print(df)
print("\nMin-Max Normalized Data:")
print(df_minmax)
```
<h3>2. Z-Score Normalization (Standardization)</h3>
<p>
Z-Score Normalization (Standardization) scales the data to have a mean of 0 and a standard deviation of 1.<br>
The formula for Z-Score Normalization is:<br>

𝑋′= 𝑋 − 𝜇 / 𝜎 <br>

Where:𝑋′  is the normalized value.<br>
      X is the original value.<br>
      μ is the mean of the feature<br>.
      σ is the standard deviation of the feature.<br>
      </p>
#### Example
```.py
from sklearn.preprocessing import StandardScaler

# Initialize Standard Scaler
scaler = StandardScaler()

# Apply Z-Score Normalization
df_standardized = pd.DataFrame(scaler.fit_transform(df), columns=df.columns)

print("Original Data:")
print(df)
print("\nZ-Score Normalized Data:")
print(df_standardized)
```
The other methods are not widely use but will briefly mention them.

<h3>3. MaxAbs Scaling</h3>
MaxAbs Scaling scales each feature by its maximum absolute value. It is similar to Min-Max Scaling, but it preserves the sparsity of the data, making it useful for data with a large number of zero values.

<h3>4. Robust Scaling</h3>
Robust Scaling uses the median and the interquartile range (IQR) to scale the data. It is robust to outliers and can handle skewed data better than Min-Max or Z-Score Normalization.

<h3>5. Decimal Scaling</h3>
Decimal Scaling normalizes the data by shifting the decimal point of values. The number of decimal points to shift depends on the maximum absolute value of the data. Decimal Scaling is not commonly used but can be effective for specific use cases.

<h3>6. Normalizer (L1 and L2 Normalization)</h3>
<p>
Normalization scales each data point to have a unit norm, focusing on individual samples rather than features. It is particularly useful when dealing with sparse data or when the direction of data points matters more than their magnitude.<br>

There are two types of normalization:<br>
</p>
<h4>. L1 Normalization:</h4> Scales each data point so that the sum of absolute values equals 1.
<h4>. L2 Normalization:</h4> Scales each data point so that the sum of squares equals 1 (unit norm).

<h3>Dummy Variables</h3>
<p>
Dummy variables are a technique used in statistical modeling and machine learning to include categorical data into regression models or other algorithms that require numerical input. They are particularly useful when you have categorical features with no intrinsic ordering or numerical meaning, and you need to convert these categories into a format that can be used in calculations.<br>

<b>Function of Dummy Variables:</b><br>
<i>1. Numerical Representation:</i> Dummy variables convert categorical data into a numerical form. Each category of a categorical variable is represented by a binary (0 or 1) variable.

<i>2. Avoiding Multicollinearity:</i> While converting categorical variables, one category is typically left out to prevent multicollinearity in the dataset. This is known as the "reference category."

<i>3. Interpretation:</i> They allow models to interpret the impact of different categories on the target variable.

#### Example:
Let's consider a simple dataset with a categorical variable that we want to convert into dummy variables using Python.
```.py
import pandas as pd

# Sample dataset
data = {
    'ID': [1, 2, 3, 4, 5],
    'City': ['New York', 'Los Angeles', 'Chicago', 'New York', 'Chicago'],
    'Age': [25, 34, 28, 45, 22],
    'Income': [70000, 80000, 50000, 120000, 55000]
}

df = pd.DataFrame(data)

# Display the original dataframe
print("Original DataFrame:")
print(df)

# Convert the 'City' column into dummy variables
df_dummies = pd.get_dummies(df, columns=['City'], drop_first=True)

# Display the dataframe with dummy variables
print("\nDataFrame with Dummy Variables:")
print(df_dummies)
```
#### Original DataFrame:
```.sql
-- Create a new table with dummy variables
SELECT 
    ID, 
    Age, 
    Income,
    -- Create dummy variable for Los Angeles
    CASE 
        WHEN City = 'Los Angeles' THEN 1 
        ELSE 0 
    END AS City_Los_Angeles,
    -- Create dummy variable for New York
    CASE 
        WHEN City = 'New York' THEN 1 
        ELSE 0 
    END AS City_New_York
FROM 
    cities;
```
#### DataFrame with Dummy Variables:
```.sql
-- Create a new table with dummy variables
CREATE TABLE cities_with_dummies AS
SELECT 
    ID, 
    Age, 
    Income,
    CASE 
        WHEN City = 'Los Angeles' THEN 1 
        ELSE 0 
    END AS City_Los_Angeles,
    CASE 
        WHEN City = 'New York' THEN 1 
        ELSE 0 
    END AS City_New_York
FROM 
    cities;
```
