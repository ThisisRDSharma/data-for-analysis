openExample('mrm/CreditScorecardValidationMetricsExample')
cvc


from optbinning import BinningProcess
import pandas as pd

# Example data
data = pd.DataFrame({
    'var1': [1, 2, 3, 4, 5, 6, 7, 8, 9],
    'var2': [10, 15, 20, 25, 30, 35, 40, 45, 50],
    'target': [0, 1, 0, 1, 0, 1, 0, 1, 0]
})

# Initialize BinningProcess
binning_process = BinningProcess(variable_names=['var1', 'var2'], target_name='target')

# Fit and transform
binning_process.fit(data)
binned_data = binning_process.transform(data)

# Get the binning information
binning_table = binning_process.binning_table

print(binning_table)




# Perform optimal binning
optimal_edges, criteria_values = optimal_binning(data, predictor='X', target='y', bins=4)

print("Optimal bin edges:", optimal_edges)
print("Criteria values:", criteria_values)

# Bin data based on optimal edges
data['X_binned'] = pd.cut(data['X'], bins=optimal_edges, labels=False)

print("Binned data:")
print(data)







from scipy.stats import chi2_contingency

def optimal_binning(data, predictor, target, bins=4):
    # Sort data by predictor variable
    data_sorted = data.sort_values(by=predictor)
    X_sorted = data_sorted[predictor].values
    y_sorted = data_sorted[target].values

    # Initialize arrays to store optimal bin edges and criteria values
    bin_edges = [X_sorted[0]]  # Start with the minimum value as the first bin edge
    criteria_values = []

    # Iterate through sorted values to find optimal bin edges
    for i in range(1, bins):
        # Calculate criterion (e.g., chi-square) for potential split points
        split_points = np.linspace(X_sorted[0], X_sorted[-1], num=bins+1)[1:-1]
        criteria = []

        for split_point in split_points:
            obs_table = pd.crosstab(X_sorted <= split_point, y_sorted)
            chi2, _, _, _ = chi2_contingency(obs_table)
            criteria.append(chi2)

        # Find optimal split point based on criterion
        optimal_split_point = split_points[np.argmax(criteria)]
        bin_edges.append(optimal_split_point)
        criteria_values.append(max(criteria))

        # Update y_sorted to reflect new bins
        y_sorted[X_sorted <= optimal_split_point] = i - 1

    return bin_edges, criteria_values

