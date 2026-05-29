# Index

${toc}

# BMI calculations setup

```math
# Data
// Person 1 body measurements  data
weight = 70
height = 1.86
waist = 79
hip = 92
// weight, height, waist, hip
p1 = [70, 1.86, 79, 92]

# General data structures
ps = [p1]
# Helper logic
num_rows = size(ps)[1]
row_indices = range(1, num_rows)
col_indices = range(1, 2)
bmi_data = subset(ps, index(row_indices, col_indices))
# Extract Column 1 and Column 2 as vectors
col1 = subset(ps, index(range(1, num_rows), 1))
col2 = subset(ps, index(range(1, num_rows), 2))
col3 = subset(ps, index(range(1, num_rows), 3))
col4 = subset(ps, index(range(1, num_rows), 4))
# Helper functions
rangeSwitch(val, thresholds, results) = results[sum(number(val >= thresholds))]

# Main functions
bmi(weight, height) = weight / height ^ 2
bmi_person(arr) = bmi(arr[1], arr[2])
bmi_category(bmi) = rangeSwitch(bmi, [0, 18.5, 25, 30, 99], ['Underweight', 'Normal', 'Overweight', 'Obese'])
```

# BMI calculator

```math
bmi_p1 = bmi_person(p1)
bmi_cat_p1 = bmi_category(bmi_p1)
# Perform the computation for each pair
# This will result in a new vector: [12, 25, 33]
bmi_v = bmi(col1, col2)
```

| ++BMI++        | ++Weight category++       |
| :------------: | :-----------------------: |
| <=15           | Very severely underweight |
| >15 and <=16   | Severely underweight      |
| >16 and <=18.5 | Underweight               |
| >18.5 and <=25 | Normal (healthy weight)   |
| >25 and <=30   | Overweight                |
| >30 and <=35   | Moderately obese          |
| >35 and <=40   | Severely obese            |
| >40            | Very severely obese       |

# Waist to hip ratio calculator

```math
wth = waist / hip
men_wth = rangeSwitch(wth, [0, 0.94, 0.99], ['Low Risk', 'Moderate Risk', 'High Risk'])
women_wth = rangeSwitch(wth, [0, 0.80, 0.85], ['Low Risk', 'Moderate Risk', 'High Risk'])
wth_v = col3 / col4
# whtr_v = col3 / col2
```

| ++Category++  | ++Men++     | ++Women++    |
| :-----------: | :---------: | :----------: |
| Low Risk      | <0.95       | <0.80        |
| Moderate Risk | 0.96 to 1.0 | 0.81 to 0.85 |
| High Risk     | ≥ 1.0       | ≥ 0.86       |
