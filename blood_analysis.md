# Index

${toc}

# Blood analysis calculations setup

```math
dotPC(val, comps) = concat([val], val .* comps)
erythrogram_inputs = [15.4, 4.98, 45.7, 91.8, 30.9, 33.7, 12.6]
erythrogram_indices = range(1, size(erythrogram_inputs)[1])
wbcc_inputs = dotPC(6.050, [57.4%, 5.0%, 0.5%, 28.9%, 8.3%])
wbcc_indices = range(1, size(wbcc_inputs)[1])
platelets_inputs = [202, 11.1]
platelets_indices = range(1, size(platelets_inputs)[1])
others_inputs = [85, 0.97, 158, 56, 91, 57, 19, 18, 17]
others_indices = range(1, size(others_inputs)[1])

# General data structures
erythrogram__labels = ['Hgb', 'Eritrícios', 'Hct', 'MCV', 'MCH', 'MCHC', 'RDW']
wbcc_labels = ['Leukocytes' , 'Neutrophils', 'Eosinophils', 'Basophils', 'Lymphocytes', 'Monocytes']
platelets_labels = ['Count', 'MPV']
others_labels = ['Glucose', 'Creatinine', 'Total Cholesterol', 'HDL Cholesterol', 'LDL Cholesterol', 'Triglycerides', 'TGO', 'TGP', 'GGT']

# Conditionals
isSmallerX(x) = anon(y) = y < x
isLargerX(x) = anon(y) = y > x
between(a,b) = anon(x) = a < x < b
between_lc(a,b) = anon(x) = a <= x < b
between_uc(a,b) = anon(x) = a < x <= b
between_luc(a,b) = anon(x) = a <= x <= b
hgb_c = between_luc(13.2, 16.6)
erits_c = between_luc(4.35, 5.65)
hct_c = between_luc(38.3, 48.6)
mcv_c = between_luc(78.2, 97.9)
mch_c = between_luc(26.5, 32.6)
mchc_c = between_luc(32.0, 36.5)
rdw_c = between_luc(11.8, 14.5)
erythrogram_checks = [hgb_c, erits_c, hct_c, mcv_c, mch_c, mchc_c, rdw_c]
leuk_c = between_luc(3.400, 9600)
neut_c = between_luc(1.560, 6.450)
eosi_c = between_luc(0.030, 0.480)
baso_c = between_luc(0.010, 0.080)
lymp_c = between_luc(0.950, 3.070)
mono_c = between_luc(0.260, 0.810)
wbcc_checks = [leuk_c, neut_c, eosi_c, baso_c, lymp_c, mono_c]
count_c = between_luc(135, 317)
mpv_c = between_luc(9.3, 12.1)
platelets_checks = [count_c, mpv_c]
gluco_c = between_luc(60, 110)
creat_c = between_luc(0.60, 1.20)
tcol_c = isSmallerX(200)
hdlc_c = isLargerX(60)
ldlc_c = isSmallerX(100)
trig_c = isSmallerX(150)
tgo_c = isSmallerX(34)
tgp_c = between_luc(10, 49)
ggt_c = isSmallerX(73)
others_checks = [gluco_c, creat_c, tcol_c, hdlc_c, ldlc_c, trig_c, tgo_c, tgp_c, ggt_c]
```

# Blood analysis calculator

```math
erythrogram_analysis = map(erythrogram_indices, f(i) = erythrogram_checks[i](erythrogram_inputs[i]))
wbcc_analysis = map(wbcc_indices, f(i) = wbcc_checks[i](wbcc_inputs[i]))
platelets_analysis = map(platelets_indices, f(i) = platelets_checks[i](platelets_inputs[i]))
others_analysis = map(others_indices, f(i) = others_checks[i](others_inputs[i]))
erythrogram_allgood = sum(erythrogram_analysis) == size(erythrogram_inputs)[1]
wbcc_allgood = sum(wbcc_analysis) == size(wbcc_inputs)[1]
platelets_allgood = sum(platelets_analysis) == size(platelets_inputs)[1]
others_allgood = sum(others_analysis) == size(others_inputs)[1]
```
