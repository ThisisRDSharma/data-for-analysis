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

