# Module 3 — AI for Data Analysis

**Duration:** Week 3 (~8-10 hours)
**Outcome:** Use AI to clean data, choose statistical tests, and verify bioinformatics analyses — without corrupting your results.

---

## Why this module matters

Biologists spend **20-30% of research time** analyzing data. AI can:
- Clean messy spreadsheets in minutes
- Suggest the right statistical test
- Help with bioinformatics queries

But AI can also:
- Suggest the WRONG statistical test (catastrophic for your paper)
- Fabricate gene names (catastrophic for primer design)
- Misinterpret your data (catastrophic for conclusions)

By end of this module, you'll be able to use AI confidently AND catch its mistakes.

---

## 📖 Lessons

### Lesson 3.1 — Spreadsheet Intelligence (60 min)
- Cleaning messy experimental data with AI prompts
- Quick pivot tables, normalization formulas
- **Lab 3.1:** Turn raw qPCR data into a publishable figure description

### Lesson 3.2 — Statistics Without Tears (75 min)
- Choosing the right test (t-test vs ANOVA vs non-parametric)
- Using AI to explain statistical concepts
- **Red flag:** When AI recommends the wrong test for your data type
- **Lab 3.2:** Given 4 datasets, choose the correct test

### Lesson 3.3 — Bioinformatics Assistance (90 min)
- BLAST queries, primer design help
- Protein sequence interpretation
- **⚠️ CRITICAL:** AI hallucinates gene names — always verify in UniProt
- **Lab 3.3:** Design 3 primer pairs, verify each in NCBI Primer-BLAST

### Lesson 3.4 — Interpreting AI Analysis (60 min)
- Sanity-checking AI's interpretation of your data
- When to trust AI patterns vs when to use domain knowledge
- **Lab 3.4:** Compare AI's interpretation vs yours — where do you disagree?

---

## 🧪 Labs

| Lab | Topic | Time | Difficulty |
|-----|-------|-----:|------------|
| **Lab 3.1** | Clean raw qPCR data, normalize, export for stats | 75 min | 🟡 |
| **Lab 3.2** | Choose correct statistical test for 4 datasets | 60 min | 🔴 |
| **Lab 3.3** | Design 3 primer pairs + verify in NCBI | 90 min | 🔴 |
| **Lab 3.4** | Compare AI vs human data interpretation | 75 min | 🟡 |

---

## 🎯 Module 3 deliverables

- [ ] Lab 3.1: Cleaned dataset + figure description draft
- [ ] Lab 3.2: Statistical test choice + justification (4 cases)
- [ ] Lab 3.3: 3 verified primer pairs (NCBI-verified)
- [ ] Lab 3.4: Interpretation comparison document

---

## 🇮🇳 India-specific content

### Indian statistical software access
- **R / RStudio** — free, widely used in Indian bioinformatics
- **Python (Anaconda)** — free, growing in Indian labs
- **GraphPad Prism** — paid (~₹30K/year); check if your institute has license
- **SPSS** — many Indian universities have site licenses
- **MS Excel** — surprisingly powerful for basic stats; avoid for advanced

### NCBI India mirror
- Faster access from India: https://www.ncbi.nlm.nih.gov/ (main) or via ERNET India
- BLAST, Primer-BLAST, Gene — all free
- **Indian Mirror:** https://blast.ncbi.nlm.nih.gov/ (works well from India)

### Indian bioinformatics databases
- **DBT (Department of Biotechnology)** — https://dbt.gov.in/ (covers all DBT programs incl. BTISnet, Genome India)
- **Indian Biological Data Centre** — https://ibdc.dbtindia.gov.in/ (working mirror)
- **DBT e-Library** — https://dbt.gov.in/scientific-programmes (search publications)

### Common Indian data analysis pitfalls
1. **Power cuts during experiments** → missing time points → need robust statistical handling
2. **Monsoon humidity** → affects weighing, pH meters → log environmental conditions
3. **Imported reagents** → batch variation → always include batch as covariate
4. **Lab rotation of students** → inter-operator variability → standardize protocols

---

## ⚠️ Critical warnings

### 🚨 AI hallucinates gene names
**Real example:** Asking ChatGPT for "human cancer gene symbols" can return:
- `TP53` ✅ (real)
- `BRCA1` ✅ (real)
- `MYC1` 🚨 (real but wrong — should be MYC)
- `P53R2` ✅ (real but rare)
- `MAGE-A1` ✅ (real)
- `KRASA` 🚨 (fabricated — actual is KRAS)

**Always verify in UniProt before ordering primers.**

### 🚨 AI chooses wrong statistical test
**Common mistake:** AI suggests ANOVA for n=2 groups (should be t-test).

**The 4-question test:**
1. How many groups? (2 → t-test/Wilcoxon; 3+ → ANOVA/Kruskal-Wallis)
2. Paired or unpaired? (paired → paired test)
3. Normal distribution? (no → non-parametric)
4. Equal variances? (no → Welch's t-test)

### 🚨 AI misinterprets p-values
- p < 0.05 ≠ "significant effect"
- p > 0.05 ≠ "no effect" (could be underpowered)
- Multiple comparisons → need correction (Bonferroni, FDR)
- **Always state effect size + confidence interval, not just p-value**

---

## 🔧 Tools used

| Tool | Use | Free? |
|------|-----|-------|
| **Claude / ChatGPT** | Data cleaning prompts, stats explanation | ✅ |
| **R + RStudio** | Statistical analysis, plotting | ✅ |
| **Python (pandas, scipy)** | Data wrangling, statistics | ✅ |
| **GraphPad Prism** | Quick stats, publication-quality plots | ❌ (paid) |
| **NCBI BLAST / Primer-BLAST** | Sequence verification | ✅ |
| **UniProt** | Gene/protein verification | ✅ |
| **G*Power** | Sample size & power analysis | ✅ |
| **Google Sheets** | Basic data exploration | ✅ |

---

## 📊 Self-assessment

Before moving to Module 4:
- [ ] I can clean a messy spreadsheet in 30 minutes
- [ ] I can choose the correct statistical test for any dataset
- [ ] I can verify a gene name in UniProt in 30 seconds
- [ ] I can identify when AI is misinterpreting my data

---

**Next:** [Module 4: AI for Scientific Writing →](../04-scientific-writing/README.md)