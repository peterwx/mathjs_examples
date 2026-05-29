```math
// 1. FUNCTION DEFINITIONS (Top of File)

// Comparator Factory
// Input: The matrix you want to sort (target_matrix)
// Output: A comparator function (i, j) -> number that uses that specific matrix.
// This creates a 'closure' that captures the correct matrix when called.
get_x_comparator(target_matrix) = anon(i, j) = sum(subset(target_matrix, index(i, 1))) - sum(subset(target_matrix, index(j, 1)))
// 2. DATA VARIABLES (Bottom of File)
// Row Indices (1D Array)
idx_rows = [1, 2, 3]
cols_all = [1, 2]

// Polygon A (The Real Data)
Poly_A = matrix([[100, 50], [10, 5], [2, 1]])

// 3. EXECUTION
// Step A: Generate a specific comparator for Poly_A
// We call the factory, passing the real data.
// 'comp_for_A' now holds a function permanently bound to Poly_A.
comp_for_A = get_x_comparator(Poly_A)

// Step B: Sort Indices using the generated comparator
sorted_idx = sort(idx_rows, comp_for_A)

// Step C: Reorder Matrix
Poly_A_Sorted = subset(Poly_A, index(sorted_idx, cols_all))
```