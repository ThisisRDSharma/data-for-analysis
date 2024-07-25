import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Example: Load a sample dataset (replace with your dataset loading code)
data = {
    'A': [1.2, 2.5, 3.3, 4.1, 5.7, 6.2, 7.3, 8.5, 9.0, 10.1]
}

# Convert the dictionary to a pandas DataFrame
df = pd.DataFrame(data)

# Select the column for which you want to fit the normal distribution
column_name = 'A'
column_data = df[column_name]

# Calculate mean and standard deviation of the column
mu = column_data.mean()
sigma = column_data.std()

# Generate a range of x values for plotting the PDF
x = np.linspace(column_data.min(), column_data.max(), 100)
pdf = norm.pdf(x, mu, sigma)

# Plot the histogram of the data
plt.hist(column_data, bins=5, density=True, alpha=0.6, color='g', label='Histogram')

# Plot the PDF
plt.plot(x, pdf, 'k-', linewidth=2, label='Normal Distribution')

# Add labels and title
plt.xlabel(column_name)
plt.ylabel('Probability Density')
plt.title('Normal Distribution Fit')
plt.legend()

# Show the plot
plt.grid(True)
plt.show()
