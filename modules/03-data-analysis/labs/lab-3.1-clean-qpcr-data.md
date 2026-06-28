# Lab 3.1 — Clean Real qPCR Data with AI

**Time:** 75 minutes
**Difficulty:** 🟡 Medium
**Tools:** Claude (or ChatGPT), Google Sheets, Python (optional)

---

## 🎯 Objective

Take a messy real-world qPCR dataset and turn it into analysis-ready normalized data using AI — then verify every step.

---

## 📋 What you'll submit

1. **Raw data file** (provided below)
2. **Cleaning log** — every change AI made, with justification
3. **Cleaned CSV** with calculated ΔCq, ΔΔCq, and fold change
4. **Verification report** — 5 random values checked manually
5. **Plot** showing fold change across conditions

---

## 📊 The dataset (real-style, messy on purpose)

You're studying the effect of Drug X on **BAX gene expression** (pro-apoptotic) in cancer cells, with **GAPDH** as housekeeping.

You ran a 96-well qPCR plate with:
- 4 conditions: Control (DMSO), Drug X 1μM, Drug X 10μM, Drug X 100μM
- 6 biological replicates per condition
- Each sample in triplicate (technical replicates) for BAX and GAPDH
- Plate ran on a Bio-Rad CFX96

### Raw data (copy to a CSV):

```csv
Well,Sample_ID,Condition,Replicate,Target,Cq,Notes
A1,S1,Control,1,BAX,24.32,
A2,S1,Control,1,GAPDH,18.45,
A3,S1,Control,2,BAX,24.18,
A4,S1,Control,2,GAPDH,18.52,
A5,S1,Control,3,BAX,N/A,Replicate failed
A6,S1,Control,3,GAPDH,18.48,
B1,S2,Control,1,BAX,23.98,
B2,S2,Control,1,GAPDH,18.41,
B3,S2,Control,2,BAX,24.05,
B4,S2,Control,2,GAPDH,18.55,
B5,S2,Control,3,BAX,24.12,
B6,S2,Control,3,GAPDH,18.39,
C1,S3,Control,1,BAX,24.55,
C2,S3,Control,1,GAPDH,18.62,
C3,S3,Control,2,BAX,24.47,
C4,S3,Control,2,GAPDH,18.58,
C5,S3,Control,3,BAX,24.39,
C6,S3,Control,3,GAPDH,18.51,
D1,S4,Drug_1uM,1,BAX,25.12,
D2,S4,Drug_1uM,1,GAPDH,18.49,
D3,S4,Drug_1uM,2,BAX,25.08,
D4,S4,Drug_1uM,2,GAPDH,18.55,
D5,S4,Drug_1uM,3,BAX,25.21,
D6,S4,Drug_1uM,3,GAPDH,18.43,
E1,S5,Drug_1uM,1,BAX,24.85,
E2,S5,Drug_1uM,1,GAPDH,18.47,
E3,S5,Drug_1uM,2,BAX,24.92,
E4,S5,Drug_1uM,2,GAPDH,18.52,
E5,S5,Drug_1uM,3,BAX,24.78,
E6,S5,Drug_1uM,3,GAPDH,18.41,
F1,S6,Drug_1uM,1,BAX,25.03,
F2,S6,Drug_1uM,1,GAPDH,18.53,
F3,S6,Drug_1uM,2,BAX,24.97,
F4,S6,Drug_1uM,2,GAPDH,18.48,
F5,S6,Drug_1uM,3,BAX,38.42,Possible outlier - high Cq
F6,S6,Drug_1uM,3,GAPDH,18.45,
G1,S7,Drug_10uM,1,BAX,27.85,
G2,S7,Drug_10uM,1,GAPDH,18.51,
G3,S7,Drug_10uM,2,BAX,27.92,
G4,S7,Drug_10uM,2,GAPDH,18.49,
G5,S7,Drug_10uM,3,BAX,28.04,
G6,S7,Drug_10uM,3,GAPDH,18.55,
H1,S8,Drug_10uM,1,BAX,27.74,
H2,S8,Drug_10uM,1,GAPDH,18.43,
H3,S8,Drug_10uM,2,BAX,27.81,
H4,S8,Drug_10uM,2,GAPDH,18.47,
H5,S8,Drug_10uM,3,BAX,27.89,
H6,S8,Drug_10uM,3,GAPDH,18.51,
A7,S9,Drug_10uM,1,BAX,28.21,
A8,S9,Drug_10uM,1,GAPDH,18.62,
A9,S9,Drug_10uM,2,BAX,28.15,
A10,S9,Drug_10uM,2,GAPDH,18.58,
A11,S9,Drug_10uM,3,BAX,28.08,
A12,S9,Drug_10uM,3,GAPDH,18.51,
B7,S10,Drug_100uM,1,BAX,31.45,
B8,S10,Drug_100uM,1,GAPDH,18.55,
B9,S10,Drug_100uM,2,BAX,31.52,
B10,S10,Drug_100uM,2,GAPDH,18.61,
B11,S10,Drug_100uM,3,BAX,31.38,
B12,S10,Drug_100uM,3,GAPDH,18.49,
C7,S11,Drug_100uM,1,BAX,30.98,
C8,S11,Drug_100uM,1,GAPDH,18.52,
C9,S11,Drug_100uM,2,BAX,31.05,
C10,S11,Drug_100uM,2,GAPDH,18.58,
C11,S11,Drug_100uM,3,BAX,31.12,
C12,S11,Drug_100uM,3,GAPDH,18.46,
D7,S12,Drug_100uM,1,BAX,31.28,
D8,S12,Drug_100uM,1,GAPDH,18.49,
D9,S12,Drug_100uM,2,BAX,31.34,
D10,S12,Drug_100uM,2,GAPDH,18.55,
D11,S12,Drug_100uM,3,BAX,31.41,
D12,S12,Drug_100uM,3,GAPDH,18.53,
```

**Issues to spot:**
- 1 missing value (A5: BAX, S1, Replicate 3 = "N/A")
- 1 likely outlier (F5: BAX Cq=38.42, while other Drug 1μM replicates are ~25)
- "Drug_1uM", "Drug_10uM", "Drug_100uM" naming (should be standardized)

---

## 📝 Step-by-step instructions

### Step 1: Save raw data + describe to AI (5 min)

1. Save the above data as `qpcr_raw.csv`
2. Open Claude or ChatGPT
3. Use this prompt:

```
I have a qPCR dataset from a 96-well plate studying BAX gene expression 
(pro-apoptotic) with GAPDH as housekeeping control. 4 conditions 
(Control/Drug_1uM/Drug_10uM/Drug_100uM), 6 biological replicates per 
condition, each in triplicate (technical replicates) for both BAX and GAPDH.

Attached: qpc
Issues I noticed:
- Well A5: Cq = "N/A" (replicate failed)
- Well F5: Cq = 38.42 (likely outlier - other Drug_1uM BAX replicates are ~25)
- Condition labels: "Drug_1uM", "Drug_10uM", "Drug_100uM" (should I standardize?)

Please help me:
1. QC each replicate (flag failed replicates, outliers)
2. Calculate mean Cq per sample per target
3. Calculate ΔCq = Cq(BAX) - Cq(GAPDH) per sample
4. Calculate ΔΔCq = ΔCq(sample) - mean(ΔCq) of Control group
5. Calculate fold change = 2^(-ΔΔCq)
6. Output cleaned CSV

Output columns should be:
Sample_ID, Condition, Mean_Cq_BAX, Mean_Cq_GAPDH, ΔCq, ΔΔCq, Fold_Change, QC_Flag

Also: should I exclude the outlier at F5? Include it? Treat it as missing?
```

### Step 2: Apply AI suggestions (20 min)

AI will give you Python or R code. Apply it. You should get a cleaned CSV.

**Example expected output:**

| Sample_ID | Condition | Mean_Cq_BAX | Mean_Cq_GAPDH | ΔCq | ΔΔCq | Fold_Change | QC_Flag |
|-----------|-----------|------------:|--------------:|----:|----:|------------:|---------|
| S1 | Control | 24.25 | 18.48 | 5.77 | 0.00 | 1.00 | OK (1 rep missing) |
| S2 | Control | 24.05 | 18.45 | 5.60 | -0.17 | 1.13 | OK |
| S3 | Control | 24.47 | 18.57 | 5.90 | 0.13 | 0.91 | OK |
| ... | ... | ... | ... | ... | ... | ... | ... |

### Step 3: Verify the outlier handling (10 min)

**Critical:** How did AI handle the F5 outlier (Cq = 38.42)?

**Decision matrix:**

| Scenario | Action |
|----------|--------|
| Outlier due to failed reaction (no amplification curve) | Exclude with justification |
| Outlier due to pipetting error | Exclude with justification |
| Outlier due to biological variation (rare but real) | Include + flag in figure |
| Not sure why it's an outlier | **Run the experiment again** |

**For this lab:** F5 is likely a failed reaction (Cq much higher than other replicates of same sample). **Exclude it.** Document in cleaning log.

### Step 4: Verify 5 random values manually (15 min)

Pick 5 random rows from cleaned data. Manually compute what ΔCq, ΔΔCq, and fold change should be. Compare to AI's output.

**Example verification for S1:**
- BAX replicates: 24.32, 24.18, [N/A] → Mean = (24.32 + 24.18)/2 = 24.25 ✅
- GAPDH replicates: 18.45, 18.52, 18.48 → Mean = (18.45 + 18.52 + 18.48)/3 = 18.483 ≈ 18.48 ✅
- ΔCq = 24.25 - 18.48 = 5.77 ✅
- Control mean ΔCq = (5.77 + 5.60 + 5.90 + ...) / 6 = ~5.77
- ΔΔCq for S1 = 5.77 - 5.77 = 0.00 ✅
- Fold change = 2^(-0.00) = 1.00 ✅

**Repeat for 4 more samples.**

### Step 5: Create a plot (15 min)

Use any tool (Excel, Google Sheets, R, Python). Make a bar plot of:
- X-axis: Condition (Control, Drug 1μM, Drug 10μM, Drug 100μM)
- Y-axis: Fold change in BAX expression
- Error bars: SEM or SD
- Show individual data points (not just mean)

**Expected pattern:** Fold change should INCREASE with drug dose (BAX is pro-apoptotic, drug induces apoptosis).

### Step 6: Write the cleaning log (10 min)

Document EVERY change AI made to your data:

```markdown
## Cleaning Log

### Original issues:
- 1 missing value: A5 (BAX, S1, Replicate 3) = "N/A"
- 1 likely outlier: F5 (BAX, S1, Replicate 3) = 38.42 (vs other Drug_1uM replicates ~25)
- Condition naming: "Drug_1uM" vs "Drug 1μM" (standardized to "Drug_1uM" for code)

### Decisions made:
1. **A5 missing value:** Excluded. Only 2 of 3 BAX replicates used for S1 mean.
   - Justification: Replicate failed (N/A indicates no amplification).

2. **F5 outlier (Cq=38.42):** Excluded. Used remaining 2 replicates for S6 mean.
   - Justification: Cq is >10 cycles higher than other Drug_1uM replicates, 
     indicating failed reaction or contamination.

3. **Condition naming:** Standardized to "Drug_1uM", "Drug_10uM", "Drug_100uM" 
   (underscore instead of space, ASCII instead of μ for code compatibility).

### Verification:
- Manually verified 5 random samples (S1, S4, S7, S10, S12)
- All calculations match AI output
- Total: 12 samples × 2 targets × 3 replicates = 72 data points
  - Excluded: 2 (1 missing, 1 outlier)
  - Used: 70 data points
  - Final samples: 12 (S1-S12)
```

---

## ✅ Success criteria

You pass this lab if:
- [ ] Cleaned CSV has correct calculations (verified manually for 5 samples)
- [ ] Outlier decision documented with justification
- [ ] Cleaning log shows every change
- [ ] Plot shows expected pattern (dose-dependent increase in BAX)
- [ ] AI suggestions were critically evaluated (not blindly accepted)

---

## 📤 What to submit

Submit a folder containing:
1. `qpcr_raw.csv` (original data, unchanged)
2. `qpcr_cleaned.csv` (your cleaned data)
3. `cleaning_log.md` (your documentation)
4. `verification_report.md` (your 5-sample manual check)
5. `fold_change_plot.png` (your bar plot)

---

## 🚀 Stretch goals

### Stretch 1: Add biological interpretation
After cleaning, write a 200-word interpretation:
- What does the fold change pattern mean biologically?
- Is the dose-dependence as expected?
- What additional experiments would you do?

### Stretch 2: Statistical analysis
Run one-way ANOVA on the ΔCq values (not fold change) across conditions. Calculate effect size (η²).

### Stretch 3: Multiple normalization genes
What if you had 2 housekeeping genes (GAPDH + ACTB)? How would you use the geometric mean for normalization?

### Stretch 4: Handle missing data differently
Re-run the analysis treating F5 as "low quality" (kept but flagged) instead of excluded. How does this change the results?

---

## ❓ Troubleshooting

**Q: AI suggested using β-actin instead of GAPDH. Should I switch?**
A: GAPDH is fine for this experiment. Switching housekeeping genes mid-analysis is bad practice. Use what you planned.

**Q: AI wants me to use a different outlier detection method. Which is right?**
A: For n=3, common methods:
- 1.5 × IQR rule (simple, conservative)
- Grubbs' test (assumes normality, n≥3)
- Visual inspection (you have small n, this is fine)

For this lab, visual inspection (Cq >> other replicates) is sufficient.

**Q: My cleaned CSV has NaN. What do I do?**
A: Check if AI handled the missing value. If it left NaN, you have 2 options:
- Exclude that sample entirely
- Use only the available replicates

Document your choice.

**Q: AI suggests Welch's t-test for outlier handling. What's that?**
A: Welch's t-test is for unequal variances. Not relevant for outlier handling. AI confused two things — push back.

---

## 📚 What's next

→ **[Lab 3.2: Choose the right statistical test for 4 datasets](./lab-3.2-statistical-test.md)**

In the next lab, you'll apply Lesson 3.2's decision tree to the cleaned qPCR data + 3 other biology datasets.

---

**Time check:** If you took more than 90 min, revisit the lessons. The labs build on lesson concepts.

Issues I noticed:
- Well A5: Cq = "N/A" (replicate failed)
- Well F5: Cq = 38.42 (likely outlier - other Drug_1uM BAX replicates are ~25)
- Condition labels: "Drug_1uM", "Drug_10uM", "Drug_100uM" (should I standardize?)

Please help me:
1. QC each replicate (flag failed replicates, outliers)
2. Calculate mean Cq per sample per target
3. Calculate ΔCq = Cq(BAX) - Cq(GAPDH) per sample
4. Calculate ΔΔCq = ΔCq(sample) - mean(ΔCq) of Control group
5. Calculate fold change = 2^(-ΔΔCq)
6. Output cleaned CSV

Output columns should be:
Sample_ID, Condition, Mean_Cq_BAX, Mean_Cq_GAPDH, ΔCq, ΔΔCq, Fold_Change, QC_Flag

Also: should I exclude the outlier at F5? Include it? Treat it as missing?
```

### Step 2: Apply AI suggestions (20 min)

AI will give you Python or R code. Apply it. You should get a cleaned CSV.

**Example expected output:**

| Sample_ID | Condition | Mean_Cq_BAX | Mean_Cq_GAPDH | ΔCq | ΔΔCq | Fold_Change | QC_Flag |
|-----------|-----------|------------:|--------------:|----:|----:|------------:|---------|
| S1 | Control | 24.25 | 18.48 | 5.77 | 0.00 | 1.00 | OK (1 rep missing) |
| S2 | Control | 24.05 | 18.45 | 5.60 | -0.17 | 1.13 | OK |
| S3 | Control | 24.47 | 18.57 | 5.90 | 0.13 | 0.91 | OK |
| ... | ... | ... | ... | ... | ... | ... | ... |

### Step 3: Verify the outlier handling (10 min)

**Critical:** How did AI handle the F5 outlier (Cq = 38.42)?

**Decision matrix:**

| Scenario | Action |
|----------|--------|
| Outlier due to failed reaction (no amplification curve) | Exclude with justification |
| Outlier due to pipetting error | Exclude with justification |
| Outlier due to biological variation (rare but real) | Include + flag in figure |
| Not sure why it's an outlier | **Run the experiment again** |

**For this lab:** F5 is likely a failed reaction (Cq much higher than other replicates of same sample). **Exclude it.** Document in cleaning log.

### Step 4: Verify 5 random values manually (15 min)

Pick 5 random rows from cleaned data. Manually compute what ΔCq, ΔΔCq, and fold change should be. Compare to AI's output.

**Example verification for S1:**
- BAX replicates: 24.32, 24.18, [N/A] → Mean = (24.32 + 24.18)/2 = 24.25 ✅
- GAPDH replicates: 18.45, 18.52, 18.48 → Mean = (18.45 + 18.52 + 18.48)/3 = 18.483 ≈ 18.48 ✅
- ΔCq = 24.25 - 18.48 = 5.77 ✅
- Control mean ΔCq = (5.77 + 5.60 + 5.90 + ...) / 6 = ~5.77
- ΔΔCq for S1 = 5.77 - 5.77 = 0.00 ✅
- Fold change = 2^(-0.00) = 1.00 ✅

**Repeat for 4 more samples.**

### Step 5: Create a plot (15 min)

Use any tool (Excel, Google Sheets, R, Python). Make a bar plot of:
- X-axis: Condition (Control, Drug 1μM, Drug 10μM, Drug 100μM)
- Y-axis: Fold change in BAX expression
- Error bars: SEM or SD
- Show individual data points (not just mean)

**Expected pattern:** Fold change should INCREASE with drug dose (BAX is pro-apoptotic, drug induces apoptosis).

### Step 6: Write the cleaning log (10 min)

Document EVERY change AI made to your data:

```markdown
## Cleaning Log

### Original issues:
- 1 missing value: A5 (BAX, S1, Replicate 3) = "N/A"
- 1 likely outlier: F5 (BAX, S1, Replicate 3) = 38.42 (vs other Drug_1uM replicates ~25)
- Condition naming: "Drug_1uM" vs "Drug 1μM" (standardized to "Drug_1uM" for code)

### Decisions made:
1. **A5 missing value:** Excluded. Only 2 of 3 BAX replicates used for S1 mean.
   - Justification: Replicate failed (N/A indicates no amplification).

2. **F5 outlier (Cq=38.42):** Excluded. Used remaining 2 replicates for S6 mean.
   - Justification: Cq is >10 cycles higher than other Drug_1uM replicates, 
     indicating failed reaction or contamination.

3. **Condition naming:** Standardized to "Drug_1uM", "Drug_10uM", "Drug_100uM" 
   (underscore instead of space, ASCII instead of μ for code compatibility).

### Verification:
- Manually verified 5 random samples (S1, S4, S7, S10, S12)
- All calculations match AI output
- Total: 12 samples × 2 targets × 3 replicates = 72 data points
  - Excluded: 2 (1 missing, 1 outlier)
  - Used: 70 data points
  - Final samples: 12 (S1-S12)
```

---

## ✅ Success criteria

You pass this lab if:
- [ ] Cleaned CSV has correct calculations (verified manually for 5 samples)
- [ ] Outlier decision documented with justification
- [ ] Cleaning log shows every change
- [ ] Plot shows expected pattern (dose-dependent increase in BAX)
- [ ] AI suggestions were critically evaluated (not blindly accepted)

---

## 📤 What to submit

Submit a folder containing:
1. `qpcr_raw.csv` (original data, unchanged)
2. `qpcr_cleaned.csv` (your cleaned data)
3. `cleaning_log.md` (your documentation)
4. `verification_report.md` (your 5-sample manual check)
5. `fold_change_plot.png` (your bar plot)

---

## 🚀 Stretch goals

### Stretch 1: Add biological interpretation
After cleaning, write a 200-word interpretation:
- What does the fold change pattern mean biologically?
- Is the dose-dependence as expected?
- What additional experiments would you do?

### Stretch 2: Statistical analysis
Run one-way ANOVA on the ΔCq values (not fold change) across conditions. Calculate effect size (η²).

### Stretch 3: Multiple normalization genes
What if you had 2 housekeeping genes (GAPDH + ACTB)? How would you use the geometric mean for normalization?

### Stretch 4: Handle missing data differently
Re-run the analysis treating F5 as "low quality" (kept but flagged) instead of excluded. How does this change the results?

---

## ❓ Troubleshooting

**Q: AI suggested using β-actin instead of GAPDH. Should I switch?**
A: GAPDH is fine for this experiment. Switching housekeeping genes mid-analysis is bad practice. Use what you planned.

**Q: AI wants me to use a different outlier detection method. Which is right?**
A: For n=3, common methods:
- 1.5 × IQR rule (simple, conservative)
- Grubbs' test (assumes normality, n≥3)
- Visual inspection (you have small n, this is fine)

For this lab, visual inspection (Cq >> other replicates) is sufficient.

**Q: My cleaned CSV has NaN. What do I do?**
A: Check if AI handled the missing value. If it left NaN, you have 2 options:
- Exclude that sample entirely
- Use only the available replicates

Document your choice.

**Q: AI suggests Welch's t-test for outlier handling. What's that?**
A: Welch's t-test is for unequal variances. Not relevant for outlier handling. AI confused two things — push back.

---

## 📚 What's next

→ **[Lab 3.2: Choose the right statistical test for 4 datasets](./lab-3.2-statistical-test.md)**

In the next lab, you'll apply Lesson 3.2's decision tree to the cleaned qPCR data + 3 other biology datasets.

---

**Time check:** If you took more than 90 min, revisit the lessons. The labs build on lesson concepts.EOF
wc -l lab-3.1-clean-qpcr-data.md
r_raw.csv

Issues I noticed:
- Well A5: Cq = "N/A" (replicate failed)
- Well F5: Cq = 38.42 (likely outlier - other Drug_1uM BAX replicates are ~25)
- Condition labels: "Drug_1uM", "Drug_10uM", "Drug_100uM" (should I standardize?)

Please help me:
1. QC each replicate (flag failed replicates, outliers)
2. Calculate mean Cq per sample per target
3. Calculate ΔCq = Cq(BAX) - Cq(GAPDH) per sample
4. Calculate ΔΔCq = ΔCq(sample) - mean(ΔCq) of Control group
5. Calculate fold change = 2^(-ΔΔCq)
6. Output cleaned CSV

Output columns should be:
Sample_ID, Condition, Mean_Cq_BAX, Mean_Cq_GAPDH, ΔCq, ΔΔCq, Fold_Change, QC_Flag

Also: should I exclude the outlier at F5? Include it? Treat it as missing?
```

### Step 2: Apply AI suggestions (20 min)

AI will give you Python or R code. Apply it. You should get a cleaned CSV.

**Example expected output:**

| Sample_ID | Condition | Mean_Cq_BAX | Mean_Cq_GAPDH | ΔCq | ΔΔCq | Fold_Change | QC_Flag |
|-----------|-----------|------------:|--------------:|----:|----:|------------:|---------|
| S1 | Control | 24.25 | 18.48 | 5.77 | 0.00 | 1.00 | OK (1 rep missing) |
| S2 | Control | 24.05 | 18.45 | 5.60 | -0.17 | 1.13 | OK |
| S3 | Control | 24.47 | 18.57 | 5.90 | 0.13 | 0.91 | OK |
| ... | ... | ... | ... | ... | ... | ... | ... |

### Step 3: Verify the outlier handling (10 min)

**Critical:** How did AI handle the F5 outlier (Cq = 38.42)?

**Decision matrix:**

| Scenario | Action |
|----------|--------|
| Outlier due to failed reaction (no amplification curve) | Exclude with justification |
| Outlier due to pipetting error | Exclude with justification |
| Outlier due to biological variation (rare but real) | Include + flag in figure |
| Not sure why it's an outlier | **Run the experiment again** |

**For this lab:** F5 is likely a failed reaction (Cq much higher than other replicates of same sample). **Exclude it.** Document in cleaning log.

### Step 4: Verify 5 random values manually (15 min)

Pick 5 random rows from cleaned data. Manually compute what ΔCq, ΔΔCq, and fold change should be. Compare to AI output.

**Example verification for S1:**
- BAX replicates: 24.32, 24.18, [N/A] → Mean = (24.32 + 24.18)/2 = 24.25 ✅
- GAPDH replicates: 18.45, 18.52, 18.48 → Mean = (18.45 + 18.52 + 18.48)/3 = 18.483 ≈ 18.48 ✅
- ΔCq = 24.25 - 18.48 = 5.77 ✅
- Control mean ΔCq = (5.77 + 5.60 + 5.90 + ...) / 6 = ~5.77
- ΔΔCq for S1 = 5.77 - 5.77 = 0.00 ✅
- Fold change = 2^(-0.00) = 1.00 ✅

**Repeat for 4 more samples.**

### Step 5: Create a plot (15 min)

Use any tool (Excel, Google Sheets, R, Python). Make a bar plot of:
- X-axis: Condition (Control, Drug 1μM, Drug 10μM, Drug 100μM)
- Y-axis: Fold change in BAX expression
- Error bars: SEM or SD
- Show individual data points (not just mean)

**Expected pattern:** Fold change should INCREASE with drug dose (BAX is pro-apoptotic, drug induces apoptosis).

### Step 6: Write the cleaning log (10 min)

Document EVERY change AI made to your data:

```markdown
## Cleaning Log

### Original issues:
- 1 missing value: A5 (BAX, S1, Replicate 3) = "N/A"
- 1 likely outlier: F5 (BAX, S1, Replicate 3) = 38.42 (vs other Drug_1uM replicates ~25)
- Condition naming: "Drug_1uM" vs "Drug 1μM" (standardized to "Drug_1uM" for code)

### Decisions made:
1. **A5 missing value:** Excluded. Only 2 of 3 BAX replicates used for S1 mean.
   - Justification: Replicate failed (N/A indicates no amplification).

2. **F5 outlier (Cq=38.42):** Excluded. Used remaining 2 replicates for S6 mean.
   - Justification: Cq is >10 cycles higher than other Drug_1uM replicates,
     indicating failed reaction or contamination.

3. **Condition naming:** Standardized to "Drug_1uM", "Drug_10uM", "Drug_100uM"
   (underscore instead of space, ASCII instead of μ for code compatibility).

### Verification:
- Manually verified 5 random samples (S1, S4, S7, S10, S12)
- All calculations match AI output
- Total: 12 samples × 2 targets × 3 replicates = 72 data points
  - Excluded: 2 (1 missing, 1 outlier)
  - Used: 70 data points
  - Final samples: 12 (S1-S12)
```

---

## ✅ Success criteria

You pass this lab if:
- [ ] Cleaned CSV has correct calculations (verified manually for 5 samples)
- [ ] Outlier decision documented with justification
- [ ] Cleaning log shows every change
- [ ] Plot shows expected pattern (dose-dependent increase in BAX)
- [ ] AI suggestions were critically evaluated (not blindly accepted)

---

## 📤 What to submit

Submit a folder containing:
1. `qpcr_raw.csv` (original data, unchanged)
2. `qpcr_cleaned.csv` (your cleaned data)
3. `cleaning_log.md` (your documentation)
4. `verification_report.md` (your 5-sample manual check)
5. `fold_change_plot.png` (your bar plot)

---

## 🚀 Stretch goals

### Stretch 1: Add biological interpretation
After cleaning, write a 200-word interpretation:
- What does the fold change pattern mean biologically?
- Is the dose-dependence as expected?
- What additional experiments would you do?

### Stretch 2: Statistical analysis
Run one-way ANOVA on the ΔCq values (not fold change) across conditions. Calculate effect size (η²).

### Stretch 3: Multiple normalization genes
What if you had 2 housekeeping genes (GAPDH + ACTB)? How would you use the geometric mean for normalization?

### Stretch 4: Handle missing data differently
Re-run the analysis treating F5 as "low quality" (kept but flagged) instead of excluded. How does this change the results?

---

## ❓ Troubleshooting

**Q: AI suggested using β-actin instead of GAPDH. Should I switch?**
A: GAPDH is fine for this experiment. Switching housekeeping genes mid-analysis is bad practice. Use what you planned.

**Q: AI wants me to use a different outlier detection method. Which is right?**
A: For n=3, common methods:
- 1.5 × IQR rule (simple, conservative)
- Grubbs test (assumes normality, n≥3)
- Visual inspection (you have small n, this is fine)

For this lab, visual inspection (Cq >> other replicates) is sufficient.

**Q: My cleaned CSV has NaN. What do I do?**
A: Check if AI handled the missing value. If it left NaN, you have 2 options:
- Exclude that sample entirely
- Use only the available replicates

Document your choice.

**Q: AI suggests Welchs t-test for outlier handling. Whats that?**
A: Welchs t-test is for unequal variances. Not relevant for outlier handling. AI confused two things — push back.

---

## 📚 What's next

→ **[Lab 3.2: Choose the right statistical test for 4 datasets](./lab-3.2-statistical-test.md)**

In the next lab, you will apply Lesson 3.2s decision tree to the cleaned qPCR data + 3 other biology datasets.

---

**Time check:** If you took more than 90 min, revisit the lessons. The labs build on lesson concepts.