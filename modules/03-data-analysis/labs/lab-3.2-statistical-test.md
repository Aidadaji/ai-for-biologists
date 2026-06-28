# Lab 3.2 — Choose the Right Statistical Test for 4 Datasets

**Time:** 60 minutes
**Difficulty:** 🔴 Hard (this is the most important stats lab)
**Tools:** Claude (or ChatGPT), R or Python, G*Power (optional)

---

## 🎯 Objective

Given 4 different biology datasets, apply the 4-question decision tree (from Lesson 3.2) to choose the correct statistical test, then run it + interpret results.

---

## 📋 What you'll submit

1. **Test selection worksheet** — for each dataset, your 4-question answers + chosen test
2. **Analysis code** (R or Python) for each dataset
3. **Results table** — test statistic, p-value, effect size, 95% CI
4. **Verification report** — sanity check each result
5. **Reflection** — when did AI suggest the wrong test? When did you override?

---

## 📊 The 4 datasets

### Dataset 1: qPCR fold change (from Lab 3.1)
- **Outcome:** Fold change in BAX expression (continuous, ratio)
- **Groups:** 4 (Control, Drug 1μM, Drug 10μM, Drug 100μM)
- **n per group:** 6 (S1-S6 per condition from Lab 3.1, but verify)
- **Design:** Unpaired (different cell cultures per condition)
- **Distribution:** Likely normal (qPCR ΔCq values usually are)
- **Variance:** Possibly unequal (drug may affect variance)

**Your task:** Apply 4-question tree → choose test → run it → interpret.

---

### Dataset 2: Tumor volume in mice
- **Outcome:** Tumor volume (mm³, continuous)
- **Groups:** 3 (Vehicle control, Drug A, Drug A + Drug B)
- **n per group:** 10 mice per group
- **Design:** Unpaired (different mice per group)
- **Distribution:** Skewed (tumor volumes are often right-skewed)
- **Variance:** Unequal (some mice respond, some don't)

**Your task:** Same — apply tree, choose test, run, interpret.

---

### Dataset 3: Before/after treatment (paired)
- **Outcome:** Blood pressure (mmHg, continuous)
- **Groups:** 2 time points (Before treatment, After 8 weeks treatment)
- **n:** 25 patients (same patients measured twice)
- **Design:** **Paired** (same patient, two measurements)
- **Distribution:** Approximately normal
- **Variance:** Equal across pairs

**Your task:** Note the paired design — different from Dataset 1.

---

### Dataset 4: Cell viability categories
- **Outcome:** Cell response (categorical: Dead / Alive / Apoptotic)
- **Groups:** 4 drug concentrations
- **n per group:** 100 cells counted per condition
- **Design:** Unpaired (different cells)
- **Distribution:** Categorical, NOT continuous

**Your task:** Different outcome type — different test family.

---

## 📝 Step-by-step instructions

### Step 1: For each dataset, answer the 4 questions (10 min)

Create a worksheet:

```markdown
## Dataset 1: qPCR fold change

### 4 Questions:
1. **How many groups?** 4 (Control, Drug 1μM, Drug 10μM, Drug 100μM)
2. **Paired or unpaired?** Unpaired (different cell cultures)
3. **Normal distribution?** Yes (qPCR ΔCq typically normal; verify with Shapiro-Wilk)
4. **Equal variances?** Unknown (verify with Levene's test)

### Chosen test: 
- If normal + equal variance: One-way ANOVA + Tukey HSD post-hoc
- If normal + unequal variance: Welch's ANOVA + Games-Howell post-hoc
- If non-normal: Kruskal-Wallis + Dunn's post-hoc

### Reasoning:
[explain in 2-3 sentences why this test fits]
```

Repeat for all 4 datasets.

### Step 2: Ask AI for confirmation (10 min)

For each dataset, use this prompt:

```
I have a biology dataset with these characteristics:
- Outcome: [type and units]
- Groups: [number and names]
- n per group: [sample size]
- Design: [paired/unpaired]
- Distribution: [normal/non-normal - if unsure, say so]
- Variance: [equal/unequal - if unsure, say so]

What statistical test should I use? Why? What assumptions do I need to check?

I will verify your recommendation against the standard 4-question decision tree 
for biology statistics.
```

**Compare AI's recommendation to YOUR answer.** If they differ, investigate why.

### Step 3: Run each test in R or Python (20 min)

**R example for Dataset 1:**

```r
# Load data
qpcr <- read.csv("qpcr_cleaned.csv")

# Check assumptions
shapiro.test(qpcr$Delta_Cq[qpcr$Condition == "Control"])  # per group
# ... for each condition

# Levene's test
library(car)
leveneTest(Delta_Cq ~ Condition, data = qpcr)

# If normal + equal variance: One-way ANOVA
anova_result <- aov(Delta_Cq ~ Condition, data = qpcr)
summary(anova_result)

# Post-hoc
TukeyHSD(anova_result)

# Effect size
library(effectsize)
eta_squared(anova_result)

# Plot
library(ggplot2)
ggplot(qpcr, aes(x=Condition, y=Delta_Cq)) +
  geom_boxplot() +
  geom_jitter(width=0.2) +
  theme_minimal()
```

**Python equivalent:**

```python
import pandas as pd
from scipy import stats
import pingouin as pg
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv("qpcr_cleaned.csv")

# Check assumptions
for cond in df['Condition'].unique():
    subset = df[df['Condition']==cond]['Delta_Cq']
    stat, p = stats.shapiro(subset)
    print(f"{cond}: Shapiro p={p:.3f}")

# Levene's test
from scipy.stats import levene
levene_stat, levene_p = levene(
    *[df[df['Condition']==c]['Delta_Cq'] for c in df['Condition'].unique()]
)
print(f"Levene's p={levene_p:.3f}")

# One-way ANOVA
import pingouin as pg
anova = pg.anova(data=df, dv='Delta_Cq', between='Condition')
print(anova)

# Post-hoc
from statsmodels.stats.multicomp import pairwise_tukeyhsd
tukey = pairwise_tukeyhsd(df['Delta_Cq'], df['Condition'])
print(tukey)

# Effect size
print(f"η² = {anova['np2'][0]:.3f}")
```

### Step 4: Interpret each result (10 min)

For each test, write:

```markdown
## Dataset 1 results

### Test: One-way ANOVA
- F-statistic: [value]
- p-value: [value]
- Effect size (η²): [value]
- Interpretation: [One sentence]

### Post-hoc (Tukey HSD):
- Control vs Drug 1μM: p=[value], sig=[yes/no]
- Control vs Drug 10μM: p=[value], sig=[yes/no]
- Control vs Drug 100μM: p=[value], sig=[yes/no]
- Drug 1μM vs Drug 10μM: p=[value], sig=[yes/no]
- Drug 1μM vs Drug 100μM: p=[value], sig=[yes/no]
- Drug 10μM vs Drug 100μM: p=[value], sig=[yes/no]

### Effect size interpretation:
η² = [value] → [small/medium/large effect]

### Biological interpretation:
[2-3 sentences: what does this mean for the biology?]
```

### Step 5: Sanity check (10 min)

For each result, verify:
- [ ] Test choice matches the 4-question tree
- [ ] Assumptions were actually checked
- [ ] Effect size + CI reported (not just p-value)
- [ ] Post-hoc done after significant ANOVA
- [ ] Plot included
- [ ] Sample size stated

### Step 6: Reflection (5 min)

Write a 200-word reflection:

```markdown
## Reflection

### When did AI suggest the wrong test?
[If any, explain why]

### When did I override AI?
[If any, explain why]

### What did I learn about statistics?
[3-5 bullet points]
```

---

## ✅ Success criteria

You pass this lab if:
- [ ] All 4 test choices match the 4-question decision tree
- [ ] Each test was actually run (with code shown)
- [ ] Results include p-value, effect size, CI
- [ ] Datasets 3 (paired) and 4 (categorical) used different test families than 1-2
- [ ] Reflection is honest about AI mistakes + your overrides

---

## 📊 Expected test choices (for self-check)

| Dataset | Outcome | Test family | Specific test |
|---------|---------|-------------|---------------|
| 1 (qPCR, 4 groups, normal) | Continuous | Parametric, >2 groups | One-way ANOVA + Tukey |
| 2 (tumor, 3 groups, skewed) | Continuous | Non-parametric, >2 groups | Kruskal-Wallis + Dunn |
| 3 (BP, paired) | Continuous | Parametric, paired | Paired t-test |
| 4 (categorical) | Categorical | Chi-square / Fisher's exact | Chi-square (if expected ≥5) |

**If AI chose differently, investigate before accepting.**

---

## 🚨 Common mistakes

### Mistake 1: Using ANOVA for paired data
ANOVA assumes independent groups. For paired data (Dataset 3), use paired t-test or repeated-measures ANOVA.

### Mistake 2: Using t-test for 3+ groups
Multiple t-tests inflate Type I error. Use ANOVA + post-hoc.

### Mistake 3: Using parametric test for categorical data
Dataset 4 has categorical outcome (Dead/Alive/Apoptotic). Use chi-square, NOT t-test.

### Mistake 4: Forgetting post-hoc after significant ANOVA
ANOVA tells you "some groups differ." Post-hoc tells you WHICH.

### Mistake 5: Reporting only p-value
Always include effect size + 95% CI.

### Mistake 6: Using t-test for non-normal data
If Shapiro-Wilk p<0.05, data is non-normal. Use Mann-Whitney instead.

---

## 🚀 Stretch goals

### Stretch 1: Power analysis
After running the test, calculate the achieved power given your n. Was it ≥80%?

### Stretch 2: Bayesian alternative
Re-run one analysis using Bayesian statistics (e.g., `BayesFactor` package in R). Compare to frequentist result.

### Stretch 3: Effect size calculation
For each test, calculate Cohen's d (pairwise) using effect size package.

### Stretch 4: Visualization
Create publication-quality plots:
- Box plots with individual points
- Violin plots with medians
- Forest plot of effect sizes

---

## ❓ Troubleshooting

**Q: AI suggested Welch's ANOVA but my Levene's test says equal variances. What do I do?**
A: Use the test that matches your DATA, not what AI prefers. If variances are equal, use standard ANOVA.

**Q: My data is non-normal. AI suggests transforming it (log, sqrt). Should I?**
A: Two options:
1. Transform + use parametric test
2. Use non-parametric test on raw data

Non-parametric is safer. Transforming changes interpretation ("effect on log scale" not "effect on original scale").

**Q: My ANOVA is significant but no post-hoc comparisons are. Why?**
A: Possible if Tukey HSD is conservative. Try Games-Howell (for Welch's ANOVA) or different post-hoc.

**Q: AI wants me to use a mixed-effects model. Too complex?**
A: For Module 3 lab, stick with simple tests (t-test, ANOVA). Mixed-effects is Module 3 stretch (if covered).

---

## 📚 What's next

→ **[Lab 3.3: Design 3 primer pairs and verify each in NCBI](./lab-3.3-primer-design.md)**

In the next lab, you'll apply Lesson 3.3's bioinformatics verification workflow.

---

**Time check:** If you took more than 90 min, that's OK for this lab — statistics is hard. Focus on getting test choice + interpretation right; code can be simpler.