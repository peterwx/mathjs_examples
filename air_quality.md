# Índice

${toc}

# `QualAr` Index [^qualar]

| Classification | PM10     | PM2.5  | NO2      | 03      | `S02`    |
| :-----------: | :------: | :----: | :------: | :-----: | :------: |
| Very good     | 0-20     | 0-10   | 0-40     | 0-80    | 0-100    |
| Good           | 21-35    | 11-20  | 41-100   | 81-100  | 101-200  |
| Average         | 36-50    | 21-25  | 101-200  | 101-180 | 201-350  |
| Weak         | 51-100   | 26-50  | 201-400  | 181-240 | 351-500  |
| Bad           | 101-1200 | 51-800 | 401-1000 | 241-600 | 501-1250 |

Class intervals are in `µg/m3` units.

```math
rangeSwitch(val, thresholds, results) = results[sum(number(val >= thresholds))];
pm10 = anon(val) = rangeSwitch(val, [0, 21, 36, 51, 101], ["Very good", "Good", "Average", "Weak", "Bad"]);

pm25 = anon(val) = rangeSwitch(val, [0, 11, 21, 26, 51], ["Very good", "Good", "Average", "Weak", "Bad"]);

no2 = anon(val) = rangeSwitch(val, [0, 41, 101, 201, 401], ["Very good", "Good", "Average", "Weak", "Bad"]);

o3 = anon(val) = rangeSwitch(val, [0, 81, 101, 181, 241], ["Very good", "Good", "Average", "Weak", "Bad"]);

so2 = anon(val) = rangeSwitch(val, [0, 101, 201, 351, 501], ["Very good", "Good", "Average", "Weak", "Bad"]);

p_checks = [pm10, pm25, no2, o3, so2];

values = [10, 100, 50, 190, 210];

v_idxs = range(1, size(valores)[1]);

qs_air = map(v_idxs, f(i) = p_checks[i](valores[i]))

// The reference scale ordered from Worst to Best
// Index 1 = "Bad", Index 5 = "Very good"
scoreScale = ["Bad", "Weak", "Average", "Good", "Very good"]

// Helper: Finds the index of a single value in the reference array
// Returns 0 if not found, otherwise 1-based index
idxOf(val, ref) = sum(number(compareText(ref, string(val)) == 0) .* range(1, size(ref)[1]))

// Main Function: Maps inputs to their indices and finds the value at the minimum index
// We use string(val) to ensure safe comparison if mixed types occur
getLowestScore(inputs, ref) = ref[min(map(inputs, f(x) = idxOf(x, ref)))]

// Testing
airScores = ["Very good", "Average", "Good"]


lowestResult = getLowestScore(airScores, scoreScale)

lowestQuality = getLowestScore(qs_air, scoreScale)


```

# Air quality warnings

++Average++:

"Children and the elderly with respiratory illnesses should limit outdoor activities."

++Weak++:

- "Patients with respiratory and cardiovascular conditions should reduce outdoor physical activity and, if symptoms worsen, contact the health hotline or a health unit."
- "Children, the elderly, and individuals with respiratory problems should minimize outdoor physical activity."
- "Avoid strenuous outdoor physical activity and exposure to other risk factors, such as tobacco smoke and irritating products containing solvents."

[^qualar]:
"The `QualAr` index is an indicator that reflects the state of ambient air quality in a given location. Through a classification expressed on a color scale, it provides guidance on how you can adapt your behaviors and actions to protect your health, especially if you belong to the most sensitive population groups.
The result of the QualAr Index—expressed through a classification ranging from 'Very Good' to 'Bad' and its corresponding color—is determined by the worst result of the pollutant(s) with the highest predicted concentration (\text{PM}_{10}, \text{PM}_{2.5}, \text{O}_3, \text{NO}_2).
The classification intervals of the QualAr index are aligned with the values established by legislation, as well as with the reference values recommended by the World Health Organization (WHO)."
> ^ Translated from European Portuguese.