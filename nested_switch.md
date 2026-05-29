```math
switchTextFn(input, keys, results) = results[sum(number(compareText(keys, input) == 0) .* range(1, size(keys)[1]))]

// Step 1: Define as proper 2D matrices (3 rows x 2 columns)
thresholds = [0, 50, 80]
allKeys = ["C1", "C2"; "C3", "C4"; "C5", "C6"]
allResults = ["Starter", "Novice"; "Pro", "Expert"; "Elite", "Legend"]

// Step 2: The Nested Logic
// Finds which row to use based on the score
rowIdx(score) = sum(number(score >= thresholds))

// Extract a specific row and flatten to 1D array
nestedSwitch(score, code) = switchTextFn(code, flatten(subset(allKeys, index(rowIdx(score), range(1, 2)))), flatten(subset(allResults, index(rowIdx(score), range(1, 2)))))

// --- TESTING ---

// Score 15 (Row 1) + Code "C2"
nestedSwitch(15, "C2")
// Output: "Novice" ✓

// Score 90 (Row 3) + Code "C5"
nestedSwitch(90, "C5")
// Output: "Elite" ✓
```