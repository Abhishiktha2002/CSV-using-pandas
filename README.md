# Step 1: Import Libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Step 2: Load the CSV file
df = pd.read_csv('sales_data.csv')  # Replace with your filename
df.head()

# Step 3: Basic Info
df.info()
df.describe()

# Step 4: Data Cleaning
# Optional steps: convert date, handle missing values
df['Date'] = pd.to_datetime(df['Date'])
df.isnull().sum()

# Step 5: Feature Engineering (Optional)
df['Total_Sale'] = df['Quantity'] * df['Price']

# Step 6: Exploratory Data Analysis (EDA)
# 1. Sales over time
df.groupby('Date')['Total_Sale'].sum().plot(figsize=(10,5), title='Total Sales Over Time')

# 2. Top-selling products
df.groupby('Product')['Total_Sale'].sum().sort_values(ascending=False).head(10).plot(kind='bar', title='Top Products')

# 3. Sales by Region
df.groupby('Region')['Total_Sale'].sum().plot(kind='pie', autopct='%1.1f%%', title='Sales by Region')

# 4. Monthly Sales Trend
df['Month'] = df['Date'].dt.to_period('M')
df.groupby('Month')['Total_Sale'].sum().plot(kind='line', marker='o', title='Monthly Sales Trend')

# Show plots
plt.tight_layout()
plt.show()

# Step 7: Insights
# (Include markdown or text cells in notebook with conclusions like)
# - Product A is the highest selling
# - Region B has the highest revenue
# - Sales peak in December
# CSV-using-pandas
