```math
// Switches global data
// nestedSwitch global data
// Define as proper 2D matrices (3 rows x 2 columns)
allKeys = ["C1", "C2"; "C3", "C4"; "C5", "C6"]
allResults = ["Starter", "Novice"; "Pro", "Expert"; "Elite", "Legend"]

// Switches helper functions
// safeSwitch helper - Calculate the raw index (0 if not found)
calcIdx(input, keys) = sum((input == keys) .* range(1, size(keys)[1]))

// safeSwitchText helper - Finds match index; if index is 0, it selects the 'default' string
matchIdx(input, keys) = sum(number(compareText(keys, input) == 0) .* range(1, size(keys)[1]))

// nestedSwitch helper - Finds which row to use based on the score
thresholds = [0, 50, 80]
rowIdx(score) = sum(number(score >= thresholds))

// Switches(switching functions definitions)
// Categorize where a name falls in the alphabet
categorize(nameCategories, alphaThresholds, currentName) = nameCategories[sum(compareText(currentName, alphaThresholds) >= 0)]

// Each condition in the list should evaluate to 0 or 1
// This returns the result corresponding to the first '1' found
multiSwitch(conditions, results) = results[sum(conditions .* (conditions == 1) .* range(1, size(conditions)[1]))]

// Thresholds: [0, 10, 20]
// If input is 15: (15 >= [0, 10, 20]) results in [1, 1, 0]
// Sum of [1, 1, 0] is 2, which picks the 2nd result.
rangeSwitch(val, thresholds, results) = results[sum(number(val >= thresholds))]

// Define a version that returns "Unknown" if no match is found
// We use max(idx, 1) so results[0] is never called
safeSwitch(input, keys, results, default) = [default, results[max(calcIdx(input, keys), 1)]][(calcIdx(input, keys) > 0) + 1]

safeSwitchText(input, keys, results, default) = [default, results[max(matchIdx(input, keys), 1)]][number(matchIdx(input, keys) > 0) + 1]

// Finds the 1-based index of a value in a list and returns the matching result
// Logic: (keys == input) creates a vector like [0, 1, 0].
// Multiplying by [1, 2, 3] and summing gives the index 2.
switchFn(input, keys, results) = results[sum((keys == input) .* range(1, size(keys)[1]))]

switchTextFn(input, keys, results) = results[sum(number(compareText(keys, input) == 0) .* range(1, size(keys)[1]))]

// Extract a specific row and flatten to 1D array
nestedSwitch(score, code) = switchTextFn(code, flatten(subset(allKeys, index(rowIdx(score), range(1, 2)))), flatten(subset(allResults, index(rowIdx(score), range(1, 2)))))

// Checks string keys first; if 0, checks numeric thresholds
masterLookup(val, sKeys, sRes, nThresh, nRes) = [rangeSwitch(number(val), nThresh, nRes), switchTextFn(val, sKeys, sRes)][number(matchIdx(val, sKeys) > 0) + 1]

// Switches testing(test examples)
// Thresholds: A, M, T
categorize(["A-L", "M-S", "T-Z"], ["A", "M", "T"], "Sampson")
// Example: Categorizing a string based on specific rules
// Rules: 1. Is it "A"? 2. Does it start with "B"? 3. Is it "C"?
myConditions = [compareText("B", "A") == 0, compareText("B", "B") == 0, compareText("B", "C") == 0]
multiSwitch(myConditions, ["Is A", "Is B", "Is C"])

// Score 15 (Row 1) + Code "C2"
nestedSwitch(15, "C2")
// Output: "Novice" ✓
// Score 90 (Row 3) + Code "C5"
nestedSwitch(90, "C5")
// Output: "Elite" ✓

// 0-9: "Low", 10-19: "Mid", 20+: "High"
rangeSwitch(15, [0, 10, 20], ["Low", "Mid", "High"])
rangeSwitch(25, [0, 10, 20], ["Low", "Mid", "High"])

safeSwitch(25, [0, 10, 20], ["Low", "Mid", "High"], -1)
safeSwitch(20, [0, 10, 20], ["Low", "Mid", "High"], "None")
safeSwitch(25, [0, 10, 20], ["Low", "Mid", "High"], "None")

safeSwitchText("B", ["A", "B"], ["Alpha", "Bravo"], "Not Found")
safeSwitchText("Z", ["A", "B"], ["Alpha", "Bravo"], "Not Found")

switchFn(20, [10, 20, 30], ["Small", "Medium", "Large"])

switchTextFn("B", ["A", "B", "C"], ["Alpha", "Bravo", "Charlie"])
```