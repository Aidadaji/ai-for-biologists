# Lesson 3.2 — Statistics Without Tears

**Duration:** 75 minutes
**Video:** [Link]
**Outcome:** Choose the right statistical test for any biology dataset, and use AI to explain stats concepts without drowning in jargon.

---

## The problem

You've cleaned your data. Now you need to test if your treatment had an effect.

You google "statistical test for biology" and get 50 conflicting answers. Your supervisor says "use ANOVA." A paper you cite used "Student's t-test." Someone on Twitter says you need a "Mann-Whitney U test."

**Which is right?**

This lesson gives you a clear decision tree and shows how AI can help you apply it.

---

## 🎯 What you'll learn

1. The 4 questions that determine your statistical test
2. How to use AI to choose + run the right test
3. How to interpret p-values correctly (and what they DON'T mean)
4. Effect sizes + confidence intervals (the part most papers skip)
5. Multiple comparison correction (when you have many groups)
6. Common Indian biology stats pitfalls + how to avoid them

---

## 🌳 The 4-question decision tree

Before choosing ANY test, answer these 4 questions about your data:

### Q1: How many groups are you comparing?

| # Groups | Test family |
|----------|-------------|
| **1 group** | One-sample t-test (vs known value) |
| **2 groups** | t-test family (or non-parametric) |
| **3+ groups** | ANOVA family (or non-parametric) |

### Q2: Are the groups paired or unpaired?

| Design | Example |
|--------|---------|
| **Unpaired** | Control mice vs treated mice (different animals) |
| **Paired** | Before vs after treatment in SAME animal |
| **Repeated measures** | Same animal measured at multiple time points |

### Q3: Is your data normally distributed?

| Distribution | Test choice |
|--------------|-------------|
| **Normal (Gaussian)** | Parametric tests (t-test, ANOVA) |
| **Non-normal** | Non-parametric tests (Mann-Whitney, Kruskal-Wallis) |

**How to check:** Shapiro-Wilk test (n < 50) or visual inspection of histogram/Q-Q plot.

### Q4: Do your groups have equal variances?

| Variances | Test choice |
|-----------|-------------|
| **Equal** | Standard t-test, standard ANOVA |
| **Unequal** | Welch's t-test, Welch's ANOVA |

**How to check:** Levene's test or Bartlett's test.

---

## 📊 The complete decision tree

```
START: What are you comparing?
│
├── 1 group vs known value?
│   └── One-sample t-test
│       └── Non-normal? → Wilcoxon signed-rank
│
├── 2 groups, unpaired, normal, equal variance?
│   └── Independent samples t-test (Student's)
│
├── 2 groups, unpaired, normal, unequal variance?
│   └── Welch's t-test
│
├── 2 groups, unpaired, non-normal?
│   └── Mann-Whitney U test (Wilcoxon rank-sum)
│
├── 2 groups, paired, normal?
│   └── Paired samples t-test
│
├── 2 groups, paired, non-normal?
│   └── Wilcoxon signed-rank test
│
├── 3+ groups, unpaired, normal, equal variance?
│   └── One-way ANOVA + post-hoc (Tukey HSD)
│
├── 3+ groups, unpaired, normal, unequal variance?
│   └── Welch's ANOVA + post-hoc (Games-Howell)
│
└── 3+ groups, unpaired, non-normal?
    └── Kruskal-Wallis + post-hoc (Dunn's)
```

---

## 🤖 Using AI to choose + run the test

### Prompt template (copy-paste and customize)

```
I'm analyzing data from a biology experiment and need help choosing the right 
statistical test.

## My experiment
[Describe: cell type, treatment, what you measured, how many groups]

## My data
- Number of groups: [e.g., 4 conditions]
- Sample size per group: [e.g., n=6 per condition]
- Paired or unpaired: [e.g., unpaired - different animals per condition]
- Outcome variable: [e.g., cell viability %]
- Distribution: [normal/non-normal - if unsure, say "not sure"]
- Variance: [equal/unequal - if unsure, say "not sure"]

## What I want
1. Recommend the appropriate statistical test(s) + justification
2. Help me check assumptions (normality, variance)
3. Run the test (Python or R code)
4. Interpret the result in plain English

Attached: [your cleaned data CSV]
```

### Example prompt (real biology use case)

```
I'm testing whether Drug X (at 3 doses: 1μM, 10μM, 100μM) reduces cancer cell 
viability compared to control (no drug). I have 6 replicates per condition 
(unpaired - different wells per condition).

Data attached: viability_cleaned.csv
Columns: Condition (Control/Drug1/Drug10/Drug100), Replicate, Pct_Viability

Please:
1. Recommend the right test
2. Check normality (Shapiro-Wilk)
3. Check variance (Levene's test)
4. Run the appropriate test
5. If significant, run post-hoc (which doses differ from which?)
6. Calculate effect sizes (Cohen's d or eta-squared)
7. Generate a publication-quality plot
```

### What AI will return (typically)

```
Recommended test: One-way ANOVA (4 unpaired groups, after checking normality 
and variance assumptions pass)

Python code:
```python
import pandas as pd
import scipy.stats as stats
from statsmodels.stats.multicomp import pairwise_tukeyhsd

df = pd.read_csv('viability_cleaned.csv')

# Check assumptions
for cond in df['Condition'].unique():
    subset = df[df['Condition']==cond]['Pct_Viability']
    shapiro_p = stats.shapiro(subset).pvalue
    print(f"{cond}: Shapiro p={shapiro_p:.3f}")

# Levene's test
levene_p = stats.levene(
    df[df['Condition']=='Control']['Pct_Viability'],
    df[df['Condition']=='Drug1']['Pct_Viability'],
    df[df['Condition']=='Drug10']['Pct_Viability'],
    df[df['Condition']=='Drug100']['Pct_Viability']
).pvalue
print(f"Levene's p={levene_p:.3f}")

# One-way ANOVA
f_stat, anova_p = stats.f_oneway(
    df[df['Condition']=='Control']['Pct_Viability'],
    df[df['Condition']=='Drug1']['Pct_Viability'],
    df[df['Condition']=='Drug10']['Pct_Viability'],
    df[df['Condition']=='Drug100']['Pct_Viability']
)
print(f"ANOVA F={f_stat:.3f}, p={anova_p:.4f}")

# Post-hoc
tukey = pairwise_tukeyhsd(df['Pct_Viability'], df['Condition'])
print(tukey)
```

Interpretation:
- One-way ANOVA shows a significant effect of Drug X on viability (F=12.4, 
  p<0.001)
- Post-hoc (Tukey HSD) shows that 10μM and 100μM doses significantly reduce 
  viability vs Control (p<0.01 each), but 1μM does not (p=0.23)
- Effect size: η² = 0.74 (large effect)
```

---

## ⚠️ Critical: What p-values DON'T mean

This is the most misunderstood concept in biology stats. **Memorize this:**

### p < 0.05 ≠ "the effect is real"
p < 0.05 means: "If there were NO effect, we'd see results this extreme only 5% of the time."

### p > 0.05 ≠ "there's no effect"
p > 0.05 means: "We don't have enough evidence to reject the null." Could be:
- No effect (true negative)
- Real effect but underpowered study (false negative — most common in biology!)

### The 4 possible outcomes

|  | Reality: Effect exists | Reality: No effect |
|--|------------------------|--------------------|
| **Test p < 0.05** | ✅ True positive | ❌ False positive (Type I error, α = 0.05) |
| **Test p > 0.05** | ❌ False negative (Type II error, β) | ✅ True negative |

### Power = 1 - β

Statistical power = probability of detecting a real effect if it exists.

**Most biology studies are UNDERPOWERED.** A study with n=3 per group has ~20% power for medium effects. n=6 has ~50%. You need n=12-20+ for 80% power.

→ Use **G*Power** (free) to calculate required n for your experiment.

---

## 📏 Effect sizes: the part everyone skips

**Effect size** tells you HOW BIG the effect is, regardless of sample size.

| Test | Effect size measure | Interpretation |
|------|---------------------|----------------|
| **t-test** | Cohen's d | 0.2 = small, 0.5 = medium, 0.8 = large |
| **ANOVA** | η² (eta-squared) | 0.01 = small, 0.06 = medium, 0.14 = large |
| **Correlation** | r | 0.1 = small, 0.3 = medium, 0.5 = large |

**Always report effect size + 95% confidence interval, not just p-value.**

Example (good):
> "Drug X reduced viability by 23% (95% CI: 15-31%, p<0.001, Cohen's d=1.4)."

Example (bad):
> "Drug X significantly reduced viability (p<0.001)."

---

## 🔬 Multiple comparisons: when to correct

If you test 5 different doses vs control, by chance **1 in 20** will be "significant" even if there's no real effect.

### When to correct

| Situation | Correction |
|-----------|------------|
| Multiple pairwise comparisons | Bonferroni or Tukey HSD |
| Many variables tested (omics) | FDR (Benjamini-Hochberg) |
| Multiple time points | Bonferroni or FDR |
| Pre-planned specific comparisons | Maybe not needed |

### Bonferroni (simple, conservative)
α_adjusted = α / n_comparisons

If you test 5 things at α=0.05, use α=0.01 per test.

### FDR (less conservative, better for many tests)
Controls the **proportion** of false discoveries. Better for omics.

**AI prompt:**
```
I'm comparing 5 doses vs control (5 t-tests). Should I apply Bonferroni 
correction? At what alpha level?
```

---

## 🇮🇳 India-specific stats pitfalls

### 1. Small sample sizes
Indian lab budgets often limit n. **Power analysis BEFORE the experiment** is critical. Most Indian theses are underpowered.

**Solution:** Use G*Power during experimental design (Module 2), not after.

### 2. Batch effects from instrument variation
Indian labs may share equipment across departments. Different days = different baselines.

**Solution:** Include batch as a covariate in your model (ANCOVA). Or randomize samples across batches.

### 3. Monsoon humidity affecting weights
Weighing chemicals during monsoon = humidity absorption. Concentrations may be off.

**Solution:** Re-weigh on dry days. Log humidity in lab notebook.

### 4. Hindi/regional Excel formulas
Some Indian researchers use Hindi Excel (Hindi numerals: १२३ instead of 123).

**Solution:** Standardize to English Excel before statistical analysis.

### 5. Power cuts during experiments
Missing time points = unbalanced data.

**Solution:** Use mixed-effects models (can handle missing data). Or repeat the experiment with backup power.

### 6. Reagent batch variation
Imported reagents come in batches. Each batch may differ.

**Solution:** Always include batch as a covariate. Test for batch effect first.

---

## 🚨 When AI gets statistics WRONG

### Error 1: Wrong test for paired data
**AI does:** Independent t-test on before/after data from same animals.
**Reality:** Should be paired t-test. Independent test loses power and inflates Type I error.

### Error 2: ANOVA without post-hoc
**AI does:** Reports "p<0.05, significant" but doesn't tell you WHICH groups differ.
**Reality:** ANOVA is an omnibus test. Need post-hoc (Tukey HSD) to identify specific differences.

### Error 3: Treating ordinal data as continuous
**AI does:** Runs t-test on "low/medium/high" dose categories.
**Reality:** Ordinal data needs non-parametric tests or special models (ordinal regression).

### Error 4: Not checking assumptions
**AI does:** Runs t-test without checking normality.
**Reality:** If data is non-normal, t-test is invalid. Need Mann-Whitney instead.

### Error 5: Ignoring multiple comparisons
**AI does:** Runs 10 t-tests, reports 3 with p<0.05.
**Reality:** With α=0.05 and 10 tests, ~0.5 false positives expected by chance. Need correction.

### Error 6: Reporting "p=0.052, trending toward significance"
**This is wrong.** p=0.052 is NOT significant. Don't torture the data.

---

## ✅ Verification checklist for AI stats

Before accepting AI's statistical output, verify:

- [ ] **Test choice:** Does it match the 4-question decision tree?
- [ ] **Assumptions checked:** Normality + variance tested?
- [ ] **Effect size reported:** Cohen's d or η² included?
- [ ] **Confidence intervals:** 95% CIs reported?
- [ ] **Multiple comparison correction:** Applied if needed?
- [ ] **Post-hoc tests:** Done after significant ANOVA?
- [ ] **Plot included:** Boxplot or violin plot to visualize?
- [ ] **Sample size stated:** n per group?
- [ ] **Biological replicates:** Not just technical replicates?

---

## 🎯 Hands-on demo

In the video, I demonstrate:
1. Choosing tests for 4 different biology datasets
2. Using AI to check assumptions (normality, variance)
3. Running the test in R
4. Calculating effect sizes
5. Creating publication-quality plots

**Watch:** [Video timestamp 32:00]

---

## 🎯 Action items

Before moving to Lesson 3.3:

- [ ] Pick one of your cleaned datasets from Lesson 3.1
- [ ] Answer the 4 questions (groups, paired, normal, variance)
- [ ] Use the AI prompt template above
- [ ] Verify the test choice matches the decision tree
- [ ] Run the test + check assumptions
- [ ] Calculate effect size + 95% CI

---

## 📚 Additional resources

- **AlterLab skills used:**
  - `alterlab-statistics` — test selection + interpretation
  - `alterlab-r-stats` — R code for common tests
  - `alterlab-effect-size` — Cohen's d, η² calculations
- **Free tools:**
  - **G*Power** — sample size + power calculations
  - **R / RStudio** — free, powerful, well-documented
  - **Python (SciPy, statsmodels)** — alternative to R
  - **JASP** — free, point-and-click statistics
- **Indian resources:**
  - **ICMR bioethics guidelines** — include statistical standards
  - **Indian Statistical Institute (ISI)** — short courses
  - **FOSSEE** (IIT Bombay) — free stats courses in regional languages

---

**Next lesson:** [Lesson 3.3 — Bioinformatics Assistance](./03-bioinformatics-assistance.md) →