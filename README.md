import pandas as pd

# Sample dataset
data = {
    'Column1': [1, 2, None, 4, 5],
    'Column2': [None, 2, 3, None, 5]
}

df = pd.DataFrame(data)
print("Original DataFrame:")
print(df)






def find_missing_values(df, col1, col2):
    # Create a mask for missing values in each column
    mask_col1 = df[col1].isnull()
    mask_col2 = df[col2].isnull()
    
    # Find the indices where there are missing values in col1 followed by non-missing values in col2
    missing_col1_followed_by_value_col2 = mask_col1 & ~mask_col1.shift(-1) & ~mask_col2.shift(-1)

    # Find the indices where there are missing values in col2 followed by non-missing values in col1
    missing_col2_followed_by_value_col1 = mask_col2 & ~mask_col2.shift(-1) & ~mask_col1.shift(-1)
    
    # Combine the indices
    missing_indices = missing_col1_followed_by_value_col2 | missing_col2_followed_by_value_col1
    
    return df[missing_indices]

missing_values_df = find_missing_values(df, 'Column1', 'Column2')
print("Rows with missing values followed by non-missing values in the other column:")
print(missing_values_df)





