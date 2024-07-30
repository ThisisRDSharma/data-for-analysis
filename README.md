import pandas as pd

# Example DataFrame
data = {
    'A': [1, None, 3, None, 5],
    'B': [None, 2, None, 4, 5],
    'C': [None, None, 3, None, 5]
}

df = pd.DataFrame(data)

columns_of_interest = ['A', 'B', 'C']

def find_missing_with_subsequent_values(df, columns):
    # Create a boolean DataFrame where True indicates a missing value
    missing_mask = df[columns].isna()
    
    # Shift the missing mask to identify if there is a non-missing value after a missing value
    shifted_mask = missing_mask.shift(-1, axis=0)
    
    # Find rows where a value is missing but followed by a non-missing value in any of the specified columns
    missing_with_subsequent = missing_mask & shifted_mask.notna()
    
    # Identify the rows with missing values that meet the criteria
    rows_with_missing_and_following = missing_with_subsequent.any(axis=1)
    
    # Return the DataFrame with rows meeting the criteria
    return df[rows_with_missing_and_following]

# Apply the function
result = find_missing_with_subsequent_values(df, columns_of_interest)

print(result)
