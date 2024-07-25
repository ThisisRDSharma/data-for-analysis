import numpy as np

# Parameters for the normal distribution
mean = 0  # Mean of the distribution
std_dev = 1  # Standard deviation of the distribution
size = 100  # Number of random numbers to generate

# Generate random numbers from a normal distribution
data = np.random.normal(mean, std_dev, size)

print(data)


import pandas as pd
import numpy as np

# Create a sample dataset (assuming you already have a dataset or DataFrame)
data = {
    'A': [1, 2, 3, 4, 5],  # Example existing data in column A
    'B': [10, 20, 30, 40, 50]  # Example existing data in column B
}

# Convert the dictionary to a pandas DataFrame
df = pd.DataFrame(data)

# Parameters for the normal distribution
mean = 0  # Mean of the distribution
std_dev = 1  # Standard deviation of the distribution
size = df.shape[0]  # Number of rows in the DataFrame

# Generate random numbers from a normal distribution
random_numbers = np.random.normal(mean, std_dev, size)

# Insert these random numbers into a new column in the DataFrame
df['C'] = random_numbers

# Display the updated DataFrame
print(df)
