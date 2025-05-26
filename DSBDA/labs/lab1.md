Data Wrangling, I
Perform the following operations using Python on any open source dataset (e.g., data.csv)
1. Import all the required Python Libraries.
2. Locate an open source data from the web (e.g., https://www.kaggle.com). Provide a clear
description of the data and its source (i.e., URL of the web site).
3. Load the Dataset into pandas dataframe.
4. Data Preprocessing: check for missing values in the data using pandas isnull(), describe()
function to get some initial statistics. Provide variable descriptions. Types of variables etc.
Check the dimensions of the data frame.
5. Data Formatting and Data Normalization: Summarize the types of variables by checking
the data types (i.e., character, numeric, integer, factor, and logical) of the variables in the
data set. If variables are not in the correct data type, apply proper type conversions.
6. Turn categorical variables into quantitative variables in Python.
   
---
### Step-by-Step Data Wrangling in Python using `iris.csv`

Let's break down each of the steps you've asked for, assuming we are working with the well-known Iris dataset (a classic dataset for machine learning and data analysis tasks).

---

### 1. Import All the Required Python Libraries

To begin, we need to import the necessary libraries. The key ones for data wrangling are:

- `pandas`: For data manipulation.
    
- `numpy`: For numerical operations.
    
- `matplotlib` and `seaborn`: For visualization (optional but helpful).
    
- `scikit-learn`: For normalization (optional but useful).
    

```python
# Importing the required libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

---

### 2. Locate an Open Source Dataset

The Iris dataset is publicly available and widely used for demonstration purposes. It is available from multiple sources like Kaggle or UCI Machine Learning Repository.

**Dataset Description:**

- **Source URL:** [Iris Dataset on Kaggle](https://www.kaggle.com/datasets/uciml/iris)
    
- **Description:** This dataset consists of 150 rows and 5 columns. The goal is to classify iris plants into 3 species based on the length and width of their sepals and petals.
    
- **Columns:**
    
    1. `sepal_length` (float): Length of the sepal (cm).
        
    2. `sepal_width` (float): Width of the sepal (cm).
        
    3. `petal_length` (float): Length of the petal (cm).
        
    4. `petal_width` (float): Width of the petal (cm).
        
    5. `species` (object): The class label (Iris-setosa, Iris-versicolor, or Iris-virginica).
        

---

### 3. Load the Dataset into a Pandas DataFrame

Now let's load the dataset into a pandas dataframe.

```python
# Load the dataset
df = pd.read_csv("path/to/iris.csv")  # Adjust the path as needed
df.head()  # Display the first few rows
```

This will give you a preview of the dataset.

---

### 4. Data Preprocessing

We’ll check for missing values, basic statistics, and variable descriptions.

#### Check for Missing Values

```python
# Check for missing values
missing_values = df.isnull().sum()
print("Missing Values:\n", missing_values)
```

#### Summary Statistics

Use the `describe()` function to get initial statistics for numerical columns.

```python
# Summary statistics
summary = df.describe()
print("Summary Statistics:\n", summary)
```

#### Variable Descriptions

- `sepal_length`: Continuous numerical variable (float)
    
- `sepal_width`: Continuous numerical variable (float)
    
- `petal_length`: Continuous numerical variable (float)
    
- `petal_width`: Continuous numerical variable (float)
    
- `species`: Categorical variable (string or object)
    

#### Dimensions of the DataFrame

```python
# Check the dimensions of the dataset
print(f"Data dimensions: {df.shape}")
```

---

### 5. Data Formatting and Normalization

#### Checking and Converting Data Types

We will check the data types of each column and convert any columns if necessary.

```python
# Checking the data types of the columns
print("Data Types:\n", df.dtypes)
```

In this case:

- The `sepal_length`, `sepal_width`, `petal_length`, and `petal_width` columns should be numeric (float).
    
- The `species` column is categorical, which is fine.
    

If any column has the wrong data type, we can convert it like this:

```python
# Convert species to categorical if it's not already
df['species'] = df['species'].astype('category')
```

#### Normalizing Data (Optional)

Normalization is important for machine learning models, especially those sensitive to feature scales. For this example, we can use `MinMaxScaler` from `scikit-learn` to normalize the numerical columns.

```python
from sklearn.preprocessing import MinMaxScaler

# Normalizing numerical columns (sepal_length, sepal_width, petal_length, petal_width)
scaler = MinMaxScaler()
df[['sepal_length', 'sepal_width', 'petal_length', 'petal_width']] = scaler.fit_transform(df[['sepal_length', 'sepal_width', 'petal_length', 'petal_width']])

print("Normalized Data:\n", df.head())
```

---

### 6. Convert Categorical Variables into Quantitative Variables

The `species` column is categorical. We can convert it into a numerical format using label encoding or one-hot encoding. Let’s use label encoding for simplicity.

```python
from sklearn.preprocessing import LabelEncoder

# Label encoding the 'species' column
encoder = LabelEncoder()
df['species'] = encoder.fit_transform(df['species'])

print("Encoded Data:\n", df.head())
```

---

### Final Result

Here’s the complete code for this data wrangling process:

```python
# Step 1: Import libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.preprocessing import MinMaxScaler, LabelEncoder

# Step 2: Load the dataset
df = pd.read_csv("path/to/iris.csv")
print("Data Loaded Successfully!\n", df.head())

# Step 3: Data Preprocessing
# Checking for missing values
missing_values = df.isnull().sum()
print("Missing Values:\n", missing_values)

# Summary Statistics
summary = df.describe()
print("Summary Statistics:\n", summary)

# Checking the data types
print("Data Types:\n", df.dtypes)

# Checking the dimensions
print(f"Data dimensions: {df.shape}")

# Step 4: Data Formatting and Normalization
# Converting species to categorical
df['species'] = df['species'].astype('category')

# Normalizing numerical columns
scaler = MinMaxScaler()
df[['sepal_length', 'sepal_width', 'petal_length', 'petal_width']] = scaler.fit_transform(df[['sepal_length', 'sepal_width', 'petal_length', 'petal_width']])

# Step 5: Convert Categorical Variables to Quantitative (Label Encoding)
encoder = LabelEncoder()
df['species'] = encoder.fit_transform(df['species'])

# Final DataFrame
print("Transformed Data:\n", df.head())
```

This code performs the following:

1. Loads and inspects the Iris dataset.
    
2. Checks for missing values, provides descriptive statistics, and prints data types.
    
3. Normalizes numerical features.
    
4. Encodes the categorical variable (`species`) into numerical values.
    

---

Let me know if you'd like more details or further steps!