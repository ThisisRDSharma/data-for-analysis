import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# Generate example data (replace this with your dataset loading)
data = np.random.normal(loc=0, scale=1, size=1000)

# Fit a normal distribution to the data
mu, std = norm.fit(data)

# Plot the histogram of the data
plt.hist(data, bins=30, density=True, alpha=0.6, color='g')

# Plot the PDF (Probability Density Function) of the fitted normal distribution
xmin, xmax = plt.xlim()
x = np.linspace(xmin, xmax, 100)
p = norm.pdf(x, mu, std)
plt.plot(x, p, 'k', linewidth=2)

# Add labels and title
plt.xlabel('Variable')
plt.ylabel('Density')
plt.title('Normal distribution fit')

# Show the plot
plt.show()
