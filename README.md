def drop_rows_with_non_missing_after_missing(df, start_col, end_col):
    """
    Drop rows where there is a non-missing value after a missing value within a specified range of columns.
    
    :param df: pandas DataFrame
    :param start_col: The starting column name for the range
    :param end_col: The ending column name for the range
    :return: DataFrame with specified rows dropped
    """
    # Define the column range
    columns_of_interest = df.loc[:, start_col:end_col]
    
    # Create a boolean DataFrame where True indicates a missing value
    missing_mask = columns_of_interest.isna()
    
    # Shift the mask to check if a non-missing value follows a missing value
    shifted_mask = missing_mask.shift(-1, axis=0)
    
    # Identify rows where missing values are followed by non-missing values in the range
    rows_with_non_missing_after_missing = missing_mask & shifted_mask.notna()
    
    # Find rows that have at least one True in the mask, indicating the presence of non-missing values after missing
    rows_to_drop = rows_with_non_missing_after_missing.any(axis=1)
    
    # Drop these rows from the original DataFrame
    filtered_df = df[~rows_to_drop]
    
    return filtered_df

# Example usage
start_col = 'A'
end_col = 'C'
filtered_df = drop_rows_with_non_missing_after_missing(df, start_col, end_col)

print(filtered_df)
