import pandas as pd
import numpy as np

# Step 1: Load the dataset
df = pd.read_csv('path_to_your_dataset.csv')

# Step 2: Handle missing values
# Option 1: Remove rows with missing values
df.dropna(inplace=True)

# Option 2: Fill missing values with a specific value (e.g., mean, median, mode)
df.fillna(df.mean(), inplace=True)

# Step 3: Remove duplicates
df.drop_duplicates(inplace=True)

# Step 4: Correct data types
# Example: Convert a column to datetime
df['date_column'] = pd.to_datetime(df['date_column'])

# Example: Convert a column to numeric (coerce invalid values to NaN)
df['numeric_column'] = pd.to_numeric(df['numeric_column'], errors='coerce')

# Step 5: Handle outliers
# Example: Remove outliers based on the IQR method
Q1 = df.quantile(0.25)
Q3 = df.quantile(0.75)
IQR = Q3 - Q1
df = df[~((df < (Q1 - 1.5 * IQR)) |(df > (Q3 + 1.5 * IQR))).any(axis=1)]

# Step 6: Standardize/normalize data (if needed)
# Example: Standardize a specific column
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
df['standardized_column'] = scaler.fit_transform(df[['numeric_column']])

# Save the cleaned dataset
df.to_csv('cleaned_dataset.csv', index=False)

print("Data cleaning completed successfully!")
