# EDA
1)import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt # visualizing data
%matplotlib inline
import seaborn as sns
numpy (np):
A library used for numerical computations, especially for handling arrays and performing mathematical operations efficiently.

pandas (pd):
A powerful library for data manipulation and analysis. It provides data structures like DataFrames for handling tabular data.

matplotlib.pyplot (plt):
A core library for creating static, interactive, and animated visualizations in Python. The alias plt is commonly used for brevity.

%matplotlib inline:
This is a magic command specific to Jupyter notebooks. It ensures that Matplotlib plots are displayed inline, directly below the code cells that generate them.

seaborn (sns):
A library built on top of Matplotlib, providing a high-level interface for creating attractive and informative statistical graphics.

2)DF = pd.read_csv("F:/Pandas/Diwali Sales Data.csv", encoding="Unicode_Escape")
DF
pd.read_csv("F:/Pandas/Diwali Sales Data.csv", encoding="Unicode_Escape"):

Purpose: Reads a CSV (Comma-Separated Values) file from the specified file path into a pandas DataFrame.
Parameters:
"F:/Pandas/Diwali Sales Data.csv": The file path to the CSV file.
encoding="Unicode_Escape": Ensures the proper handling of special characters and Unicode data in the file.
DF:

The DataFrame DF is used to store the tabular data from the CSV file.
It acts as a Python object that provides methods for data manipulation and analysis.
DF (when called):

Outputs the content of the DataFrame, displaying the first few rows or the entire data (depending on the environment).

3)DF.shape
DF.head(10)
DF.info()
DF.columns
DF.describe()
DF.shape:

Purpose: Returns a tuple representing the dimensions of the DataFrame.
Output: The first value indicates the number of rows, and the second value shows the number of columns.
Example: (1000, 10) means the dataset has 1000 rows and 10 columns.
DF.head(10):

Purpose: Displays the first 10 rows of the DataFrame.
Usage: Helps preview the dataset's structure and verify that it was loaded correctly.
Parameter: 10 specifies the number of rows to display. You can change this number as needed.
DF.info():

Purpose: Provides a concise summary of the DataFrame, including:
Column names
Data types
Non-null values in each column
Usage: Useful for quickly understanding the dataset's structure and identifying missing values.
DF.columns:

Purpose: Lists all the column names in the DataFrame.
Usage: Helpful for verifying the dataset schema or selecting specific columns for analysis.
DF.describe():

Purpose: Generates summary statistics for numerical columns, such as:
Count, mean, standard deviation, minimum, maximum, and quartiles.
Usage: Provides insights into the data distribution and helps detect potential outliers.

4)DF.drop(['Status', 'unnamed1'], axis=1, inplace=True)
DF.drop():

Purpose: Removes specified columns or rows from the DataFrame.
Parameters:
['Status', 'unnamed1']: A list of column names to be removed.
axis=1: Specifies that the operation applies to columns. (axis=0 would apply to rows.)
inplace=True: Updates the DataFrame directly without creating a new one.
Reason for Dropping Columns:

'Status' and 'unnamed1': These columns are assumed to be unrelated to the analysis or contain blank values. Removing them simplifies the dataset and reduces noise.

5)pd.isnull(DF).sum()
pd.isnull(DF):

Purpose: Detects missing or null values in the DataFrame.
Output: Returns a DataFrame of the same shape as DF, where each cell contains True if the value is null and False otherwise.
.sum():

Purpose: Sums up the True values (treated as 1) column-wise, giving the total number of missing values for each column.
Output: A series where the index represents column names and the values indicate the count of missing values in each column.

6)# Drop rows with null values
DF.dropna(inplace=True)

# Convert the 'Amount' column to integers
DF['Amount'] = DF['Amount'].astype('int')

# Check the data type of the 'Amount' column
DF['Amount'].dtypes
DF.dropna(inplace=True):

Purpose: Removes all rows containing missing or null values from the DataFrame.
Parameter:
inplace=True: Ensures the changes are applied directly to the existing DataFrame without creating a new one.
DF['Amount'] = DF['Amount'].astype('int'):

Purpose: Converts the Amount column's data type to integers for uniformity and compatibility with numerical operations.
Reason: The Amount column might initially be read as a string or float; converting it to int makes it more suitable for numerical calculations.
DF['Amount'].dtypes:

Purpose: Checks the data type of the Amount column to confirm it has been successfully converted to int.

7)# Plotting a bar chart for Gender and its count
ax = sns.countplot(x='Gender', data=DF)

# Adding labels to the bars
for bars in ax.containers:
    ax.bar_label(bars)
sns.countplot(x='Gender', data=DF):

Purpose: Creates a bar chart showing the count of each unique value in the Gender column.
Parameters:
x='Gender': Specifies the column to plot on the x-axis.
data=DF: The DataFrame containing the data.
Output: A bar chart where the x-axis represents gender categories (e.g., Male, Female) and the y-axis represents their counts.
for bars in ax.containers::

Iterates through the bar containers (the graphical elements of the bars in the chart).
ax.bar_label(bars):

Purpose: Adds a label to each bar, displaying its count.
Effect: Makes the chart more informative by directly showing the values on top of the bars

8)# Calculate total amount by gender
sales_gen = DF.groupby(['Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)

# Plotting the bar chart
sns.barplot(x='Gender', y='Amount', data=sales_gen)
DF.groupby(['Gender'], as_index=False)['Amount'].sum():

Purpose: Groups the data by the Gender column and calculates the total (sum) of the Amount column for each group.
Parameter:
as_index=False: Ensures the result is returned as a DataFrame rather than a Series.
Output: A DataFrame with genders as rows and their corresponding total amounts as a column.
.sort_values(by='Amount', ascending=False):

Purpose: Sorts the DataFrame by the Amount column in descending order to highlight the gender with the highest total amount spent.
sns.barplot(x='Gender', y='Amount', data=sales_gen):

Purpose: Plots a bar chart with:
x='Gender': Gender categories on the x-axis.
y='Amount': Total amount spent on the y-axis.
data=sales_gen: Data source for the chart.

9)# Plotting a count plot for Age Group vs Gender distribution
ax = sns.countplot(data=DF, x='Age Group', hue='Gender')

# Adding labels to the bars
for bars in ax.containers:
    ax.bar_label(bars)
sns.countplot(data=DF, x='Age Group', hue='Gender'):

Purpose: Creates a count plot showing the distribution of counts for each Age Group while differentiating between genders using the hue parameter.
Parameters:
data=DF: The DataFrame containing the dataset.
x='Age Group': Specifies that the x-axis will represent different age groups.
hue='Gender': Differentiates the counts within each age group by gender, using different colors for each gender.
for bars in ax.containers::

Iterates over the bar containers (the graphical bars for each age group and gender) in the plot.
ax.bar_label(bars):

Purpose: Adds the count value on top of each bar, providing a numerical label to show the exact count for each gender within each age group.

10)# Calculate total amount by age group
sales_age = DF.groupby(['Age Group'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)

# Plotting the bar chart
sns.barplot(x='Age Group', y='Amount', data=sales_age)
DF.groupby(['Age Group'], as_index=False)['Amount'].sum():

Purpose: Groups the data by the Age Group column and calculates the total (sum) of the Amount column for each age group.
Parameter:
as_index=False: Ensures the result is returned as a DataFrame rather than a Series.
Output: A DataFrame with age groups as rows and their corresponding total amounts as a column.
.sort_values(by='Amount', ascending=False):

Purpose: Sorts the resulting DataFrame by the Amount column in descending order to highlight the age group with the highest total amount spent.
sns.barplot(x='Age Group', y='Amount', data=sales_age):

Purpose: Plots a bar chart with:
x='Age Group': Age groups on the x-axis.
y='Amount': Total amount spent on the y-axis.
data=sales_age: Data source for the chart.

11)# Calculate total number of orders by state and get the top 10 states
sales_state = DF.groupby(['State'], as_index=False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)

# Set the figure size for the plot
sns.set(rc={'figure.figsize':(15,5)})

# Plotting the bar chart
sns.barplot(data=sales_state, x='State', y='Orders')
DF.groupby(['State'], as_index=False)['Orders'].sum():

Purpose: Groups the data by the State column and calculates the total (sum) of the Orders column for each state.
Parameter:
as_index=False: Ensures the result is returned as a DataFrame rather than a Series.
Output: A DataFrame with states as rows and their corresponding total orders as a column.
.sort_values(by='Orders', ascending=False):

Purpose: Sorts the resulting DataFrame by the Orders column in descending order, so that states with the highest number of orders appear first.
.head(10):

Purpose: Selects the top 10 states based on the number of orders.
sns.set(rc={'figure.figsize':(15,5)}):

Purpose: Sets the size of the plot, with a width of 15 and height of 5, to ensure it fits the data properly and is easily readable.
sns.barplot(data=sales_state, x='State', y='Orders'):

Purpose: Plots a bar chart with:
x='State': States on the x-axis.
y='Orders': Total number of orders on the y-axis.
data=sales_state: Data source for the chart, which contains the top 10 states and their order totals.

12)# Calculate total sales (amount) by state and get the top 10 states
sales_state = DF.groupby(['State'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)

# Set the figure size for the plot
sns.set(rc={'figure.figsize':(15,5)})

# Plotting the bar chart
sns.barplot(data=sales_state, x='State', y='Amount')
DF.groupby(['State'], as_index=False)['Amount'].sum():

Purpose: Groups the data by the State column and calculates the total (sum) of the Amount column for each state.
Parameter:
as_index=False: Ensures the result is returned as a DataFrame rather than a Series.
Output: A DataFrame with states as rows and their corresponding total sales (amount) as a column.
.sort_values(by='Amount', ascending=False):

Purpose: Sorts the resulting DataFrame by the Amount column in descending order, highlighting the states with the highest total sales first.
.head(10):

Purpose: Selects the top 10 states based on the total sales amount.
sns.set(rc={'figure.figsize':(15,5)}):

Purpose: Sets the size of the plot, with a width of 15 and height of 5, to ensure the plot is spacious and easily readable.
sns.barplot(data=sales_state, x='State', y='Amount'):

Purpose: Plots a bar chart with:
x='State': States on the x-axis.
y='Amount': Total sales (amount) on the y-axis.
data=sales_state: Data source for the chart, containing the top 10 states and their sales totals.

13)# Plotting a count plot for Marital Status distribution
ax = sns.countplot(data=DF, x='Marital_Status')

# Set the figure size for the plot
sns.set(rc={'figure.figsize':(7,5)})

# Adding labels to the bars
for bars in ax.containers:
    ax.bar_label(bars)
sns.countplot(data=DF, x='Marital_Status'):

Purpose: Creates a count plot (a type of bar chart) that visualizes the number of occurrences of each category within the Marital_Status column.
Parameters:
data=DF: The DataFrame containing the dataset.
x='Marital_Status': Specifies that the x-axis will represent different marital status categories, such as single, married, etc.
sns.set(rc={'figure.figsize':(7,5)}):

Purpose: Sets the size of the plot to ensure it fits well within the output area, with a width of 7 and height of 5.
for bars in ax.containers::

Iterates over the bar containers (the graphical bars representing different marital status categories) in the plot.
ax.bar_label(bars):

Purpose: Adds the count value on top of each bar, showing the exact number of occurrences for each marital status category.

14)# Calculate total sales by Marital Status and Gender
sales_state = DF.groupby(['Marital_Status', 'Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)

# Set the figure size for the plot
sns.set(rc={'figure.figsize':(6,5)})

# Plotting the bar chart
sns.barplot(data=sales_state, x='Marital_Status', y='Amount', hue='Gender')
DF.groupby(['Marital_Status', 'Gender'], as_index=False)['Amount'].sum():

Purpose: Groups the data by both Marital_Status and Gender columns, then calculates the total (sum) of the Amount column for each combination of marital status and gender.
Parameters:
as_index=False: Ensures the result is returned as a DataFrame rather than a Series.
Output: A DataFrame with each combination of marital status and gender, along with the total sales (amount) for that combination.
.sort_values(by='Amount', ascending=False):

Purpose: Sorts the resulting DataFrame by the Amount column in descending order, highlighting the combinations with the highest total sales first.
sns.set(rc={'figure.figsize':(6,5)}):

Purpose: Sets the size of the plot, with a width of 6 and height of 5, to ensure the plot fits the content well and is readable.
sns.barplot(data=sales_state, x='Marital_Status', y='Amount', hue='Gender'):

Purpose: Plots a bar chart with:
x='Marital_Status': Marital statuses on the x-axis.
y='Amount': Total sales (amount) on the y-axis.
hue='Gender': Differentiates the bars based on gender, allowing a comparison between male and female sales for each marital status.

15)# Set the figure size for the plot
sns.set(rc={'figure.figsize':(20,5)})

# Plotting the count plot for Occupation distribution
ax = sns.countplot(data=DF, x='Occupation')

# Adding labels to the bars
for bars in ax.containers:
    ax.bar_label(bars)
sns.set(rc={'figure.figsize':(20,5)}):

Purpose: Sets the size of the plot to ensure it is large and clear, with a width of 20 and height of 5, which helps to accommodate the potentially large number of categories in the Occupation column.
sns.countplot(data=DF, x='Occupation'):

Purpose: Creates a count plot (a type of bar chart) that visualizes the number of occurrences of each category within the Occupation column.
Parameters:
data=DF: The DataFrame containing the dataset.
x='Occupation': Specifies that the x-axis will represent the different occupation categories.
for bars in ax.containers::

Iterates over the bar containers (the graphical bars representing different occupation categories) in the plot.
ax.bar_label(bars):

Purpose: Adds the count value on top of each bar, showing the exact number of occurrences for each occupation category.

16)# Calculate total sales by Occupation
sales_state = DF.groupby(['Occupation'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)

# Set the figure size for the plot
sns.set(rc={'figure.figsize':(20,5)})

# Plotting the bar chart
sns.barplot(data=sales_state, x='Occupation', y='Amount')
DF.groupby(['Occupation'], as_index=False)['Amount'].sum():

Purpose: Groups the data by the Occupation column and calculates the total (sum) of the Amount column for each occupation.
Parameters:
as_index=False: Ensures the result is returned as a DataFrame rather than a Series.
.sort_values(by='Amount', ascending=False):

Purpose: Sorts the resulting DataFrame by the Amount column in descending order, highlighting the occupations with the highest total sales first.
sns.set(rc={'figure.figsize':(20,5)}):

Purpose: Sets the size of the plot to 20 (width) by 5 (height), ensuring the plot is wide enough to accommodate the potentially large number of occupations in the dataset.
sns.barplot(data=sales_state, x='Occupation', y='Amount'):

Purpose: Plots a bar chart where:
x='Occupation': Occupations are displayed on the x-axis.
y='Amount': Total sales (amount) are displayed on the y-axis.

17)# Set the figure size for the plot
sns.set(rc={'figure.figsize':(20,5)})

# Plotting the count plot for Product Category distribution
ax = sns.countplot(data=DF, x='Product_Category')

# Adding labels to the bars
for bars in ax.containers:
    ax.bar_label(bars)
sns.set(rc={'figure.figsize':(20,5)}):

Purpose: Sets the size of the plot to be wide and clear, with a width of 20 and height of 5, which is helpful for accommodating many product categories in the dataset.
sns.countplot(data=DF, x='Product_Category'):

Purpose: Creates a count plot (a type of bar chart) that visualizes the number of occurrences of each product category in the Product_Category column.
Parameters:
data=DF: The DataFrame containing the dataset.
x='Product_Category': Specifies that the x-axis will represent the different product categories.
for bars in ax.containers::

Purpose: Iterates over the graphical bars that represent the different product categories in the plot.
ax.bar_label(bars):

Purpose: Adds labels to the top of each bar, showing the exact number of occurrences for each product category.

18)# Calculate total sales by Product Category and select the top 10
sales_state = DF.groupby(['Product_Category'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)

# Set the figure size for the plot
sns.set(rc={'figure.figsize':(20,5)})

# Plotting the bar chart
sns.barplot(data=sales_state, x='Product_Category', y='Amount')
DF.groupby(['Product_Category'], as_index=False)['Amount'].sum():

Purpose: Groups the data by the Product_Category column and calculates the total (sum) of the Amount column for each product category.
.sort_values(by='Amount', ascending=False):

Purpose: Sorts the resulting DataFrame by the Amount column in descending order, ensuring that product categories with the highest sales are displayed first.
.head(10):

Purpose: Selects the top 10 product categories with the highest total sales.
sns.set(rc={'figure.figsize':(20,5)}):

Purpose: Sets the figure size to 20 (width) by 5 (height), ensuring that the plot is wide enough to accommodate the categories without clutter.
sns.barplot(data=sales_state, x='Product_Category', y='Amount'):

Purpose: Plots a bar chart where:
x='Product_Category': Product categories are displayed on the x-axis.
y='Amount': Total sales (amount) are displayed on the y-axis.

19)# Calculate total orders by Product ID and select the top 10
sales_state = DF.groupby(['Product_ID'], as_index=False)['Orders'].sum().sort_values(by='Orders', ascending=False).head(10)

# Set the figure size for the plot
sns.set(rc={'figure.figsize':(20,5)})

# Plotting the bar chart
sns.barplot(data=sales_state, x='Product_ID', y='Orders')
DF.groupby(['Product_ID'], as_index=False)['Orders'].sum():

Purpose: Groups the data by the Product_ID column and calculates the total number of orders (sum) for each product ID.
.sort_values(by='Orders', ascending=False):

Purpose: Sorts the resulting DataFrame by the Orders column in descending order, ensuring that the products with the highest number of orders appear first.
.head(10):

Purpose: Selects the top 10 product IDs with the highest total number of orders.
sns.set(rc={'figure.figsize':(20,5)}):

Purpose: Sets the figure size to 20 (width) by 5 (height), making the plot wide enough to display the top 10 products clearly.
sns.barplot(data=sales_state, x='Product_ID', y='Orders'):

Purpose: Plots a bar chart where:
x='Product_ID': The product IDs are displayed on the x-axis.
y='Orders': The total number of orders for each product ID is displayed on the y-axis.

20)# Set up the figure size for the plot
fig1, ax1 = plt.subplots(figsize=(12,7))

# Calculate total orders by Product_ID, select the top 10, and plot the bar chart
DF.groupby('Product_ID')['Orders'].sum().nlargest(10).sort_values(ascending=False).plot(kind='bar')
DF.groupby('Product_ID')['Orders'].sum():

Purpose: Groups the data by the Product_ID column and calculates the total number of orders (sum) for each product ID.
.nlargest(10):

Purpose: Selects the top 10 product IDs with the highest total number of orders. This function returns the largest 10 values from the dataset.
.sort_values(ascending=False):

Purpose: Sorts the resulting values in descending order to ensure that the product IDs with the highest order count are displayed first.
plt.subplots(figsize=(12,7)):

Purpose: Sets up a figure with a size of 12 (width) by 7 (height) inches. This is done to create a spacious plot that clearly displays the top 10 products.
.plot(kind='bar'):

Purpose: Plots a bar chart where:
The x-axis represents the product IDs.
The y-axis represents the total number of orders for each product ID.
The chart type is set to 'bar' for a vertical bar chart.
