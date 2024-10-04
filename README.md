# Marketing Exploratory Data & Statistical Analysis Using Python

## Project Overview
<p> This project focuses on cleaning, analyzing, and visualizing a marketing dataset to gain insights into customer demographics, purchasing behaviors, and trends. The analysis includes data cleaning, handling missing values, identifying and removing outliers, and performing feature engineering to improve the dataset for further analysis and modeling. </p>

<img align="centre" alt="coding" width="1100" src="https://cdn.analyticsvidhya.com/wp-content/uploads/2021/02/nv-ccx-02-scaled.webp">

## Dataset
<p>The dataset used for this project was sourced from <a href="https://www.kaggle.com/code/jabeen12/business-analysis-with-eda-statistics-data-vis/input" target="_blank">Kaggle</a>. It contains customer demographic and transactional information, which is useful for exploring marketing trends and behaviors. The dataset was cleaned and analyzed to create visualizations and extract insights.</p>

## Data Cleaning
#### i) Correcting Date Format:
- The Dt_Customer column contains date entries with multiple formats.
- To standardize the dates, a custom function was applied to handle different date formats (MM/DD/YY and YYYY-MM-DD) and convert them to the format YYYY-MM-DD.
- The function also handles missing values by returning NaT (Not a Time) for invalid dates.

```
# Parsing dates with different formats and correcting them
df['Dt_Customer_Corrected'] = df['Dt_Customer'].apply(parse_dates)
```
#### ii) Handling Missing Values:
- The Income column contained missing values. These values were filled by calculating the average income based on the Education level of customers.
- This method helps maintain the integrity of the dataset without introducing bias.
```
# Fill missing 'Income' values based on Education level averages
df['Income'] = df.apply(fill_missing_income, axis=1)
```
## Outlier Detection and Removal
#### i) Age and Marital Status:
- Identified outliers in the Year_Birth column to correct abnormal age entries.
- Cleaned the Marital_Status column by removing incorrect or irrelevant values such as "Absurd" "YOLO" and "Alone".

<div style="display: flex; justify-content: center; align-items: center;">
  <img src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Age%20Distribution_with_Outliers.png" alt="Age Distribution" width="500">
  <img src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Marital%20Status%20Distribution_with_Outliers.png" alt="Marital Status Distribution" width="500">
</div>

```
# Remove Marital Status outliers
filtered_data1 = filtered_data1[~filtered_data1['Marital_Status'].isin(['Alone', 'YOLO', 'Absurd'])]
```
#### ii) Income Distribution:
- Visualized the distribution of customer income to detect the presence of outliers and skewness.
- Identified and removed an outlier with an income value of 666666 for a more accurate representation.

<img align="centre" alt="coding" width="500" src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Income%20Distribution%20with%20Outliers.png">

## Feature Engineering
#### i) Total Purchases:
<p>Created a new feature Total_Purchases, representing the sum of purchases made through different channels (Web, Store, Catalog).</p>

```
# Create Total Purchases feature
filtered_data2['Total_Purchases'] = filtered_data2['NumWebPurchases'] + filtered_data2['NumStorePurchases'] + filtered_data2['NumCatalogPurchases']
```
#### ii) Income vs Spending Analysis:
<p>Analyzed the relationship between customer income and their spending on various product categories. This helps in identifying high-value customers based on their purchasing patterns.</p>

```
# Scatter plot: Income vs Total Spending
sns.scatterplot(x=filtered_data2['Income'], y=filtered_data2['Total_Spending'])
```
#### iii) Country-wise Spending on Wines:
<p>Performed an analysis of wine spending across different countries to identify regions with the highest expenditure.</p>

```
# Country-wise spending on wines
sns.barplot(x='Country', y='MntWines', data=country_wine_spending)
```
## Key Visualizations
#### 1. Income Distribution
<p>This plot shows the distribution of customer income to identify patterns and detect outliers.</p>
<img align="centre" alt="coding" width="500" src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Income%20Distribution.png">

#### 2. Recency Distribution
<p>This visualization highlights the recency of customer interactions, showing how recently customers made purchases.</p>
<img align="centre" alt="coding" width="500" src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Recency%20Distribution.png">

#### 3. Age Distribution
<p>The age distribution of customers, calculated from their year of birth, helps understand the age demographics.</p>
<img align="centre" alt="coding" width="500" src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Age%20Distribution.png">

#### 4. Total Purchase Distribution
<p>This plot displays the total number of purchases across different channels (Web, Store, and Catalog) per customer.</p>
<img align="centre" alt="coding" width="500" src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Total%20Purchase%20Distribution.png">

#### 5. Marital Status Distribution
<p>A breakdown of the number of customers by their marital status to explore customer demographics.</p>
<img align="centre" alt="coding" width="500" src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Marital%20Status%20Distribution.png">

#### 6. Web Visits Vs Purchases
<p>A scatterplot showing the relationship between the number of web visits per month and the total purchases made by customers.</p>
<img align="centre" alt="coding" width="500" src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Web%20Visits%20Vs%20Total%20Purchase.png">

#### 7. Income Vs Spending
<p>This visualization shows how customer income correlates with their total spending across various product categories.</p>
<img align="centre" alt="coding" width="500" src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Income%20Vs%20Total%20Spending.png">

#### 8. Spending Distribution by Product Category
<p>A box plot depicting the spending distribution on different product categories, allowing the identification of outliers.</p>
<img align="centre" alt="coding" width="500" src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Spending%20Distribution%20by%20Product%20Category.png">

#### 9. Average Spending by Marital Status
<p>This bar plot illustrates the average spending of customers on various product categories based on their marital status.</p>
<img align="centre" alt="coding" width="500" src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Avg%20Spending%20by%20Marital%20Status.png">

#### 10. Country Wise Spending on Wines
<p>A country-level analysis of total spending on wines, showing regional differences in customer purchasing behavior.</p>
<img align="centre" alt="coding" width="500" src="https://github.com/CharishmaKondamuri/Marketing_EDA_and_Statistical_Analysis/blob/main/Results/Country%20wise%20spending%20on%20wines.png">

## Conclusion
<p>This project demonstrates the process of cleaning and preparing a real-world dataset for further analysis. By removing outliers, handling missing values, and engineering new features, the dataset becomes more suitable for predictive modeling and deeper business insights. The visualizations and correlation analysis provide actionable insights into customer behavior, which can be used to guide marketing strategies and customer engagement efforts.</p>

