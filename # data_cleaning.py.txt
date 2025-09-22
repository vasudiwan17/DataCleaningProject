# data_cleaning.py
# Simple data cleaning example using pandas

import pandas as pd

# 1. Load dataset (replace 'dataset.csv' with your file name)
try:
    df = pd.read_csv('dataset.csv')
except FileNotFoundError:
    print("Dataset not found. Please put 'dataset.csv' in the same folder.")
    exit()

# 2. View first few rows
print("Original Dataset:")
print(df.head())

# 3. Handle missing values
# Replace missing numerical values with column mean
for column in df.select_dtypes(include='number').columns:
    df[column].fillna(df[column].mean(), inplace=True)

# Replace missing categorical values with 'Unknown'
for column in df.select_dtypes(include='object').columns:
    df[column].fillna('Unknown', inplace=True)

# 4. Remove duplicate rows
df.drop_duplicates(inplace=True)

# 5. Save cleaned dataset
df.to_csv('dataset_cleaned.csv', index=False)

print("\nData cleaning complete! 'dataset_cleaned.csv' has been created.")