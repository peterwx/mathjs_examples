```math
// Global data

// Helper functions
// Thresholds: [0, 10, 20]
// If input is 15: (15 >= [0, 10, 20]) results in [1, 1, 0]
// Sum of [1, 1, 0] is 2, which picks the 2nd result.
rangeSwitch(val, thresholds, results) = results[sum(number(val >= thresholds))]

// safeSwitchText helper - Finds match index; if index is 0, it selects the 'default' string
matchIdx(input, keys) = sum(number(compareText(keys, string(input)) == 0) .* range(1, size(keys)[1]))

safeSwitchText(input, keys, results, default) = [default, results[max(matchIdx(input, keys), 1)]][number(matchIdx(input, keys) > 0) + 1]

// Function definitions
// Categorize a column of numbers into range buckets
bulkCategorize(inputCol, thresholds, labels) = map(inputCol, f(x) = rangeSwitch(x, thresholds, labels))

// Clean a whole vector of data at once
// inputCol is a column vector [n x 1]
bulkClean(inputCol, keys, results) = map(inputCol, f(x) = safeSwitchText(x, keys, results, x))

// Replaces specific codes globally in a matrix
// If value not in keys, it keeps the original value (x)
globalReplace(dataMatrix, keys, results) = map(dataMatrix, f(x) = safeSwitchText(x, keys, results, x))

// Testing
rawNames = ["appl", "bannana", "appl", "cherry"]
mapping = ["appl", "bannana"]
correct = ["Apple", "Banana"]
cleanNames = bulkClean(rawNames, mapping, correct)

prices = [5, 15, 25, 12]
priceLabels = bulkCategorize(prices, [0, 10, 20], ["Budget", "Mid", "Luxury"])

// Example Matrix
myData = [["A1", 10]; ["B1", 20]]
globalReplace(myData, ["A1", "B1"], ["Warehouse A", "Warehouse B"])

```
