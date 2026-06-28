# Lesson 3.1 — Spreadsheet Intelligence for Biologists

**Duration:** 60 minutes
**Video:** [Link]
**Outcome:** Turn messy experimental data into clean, analysis-ready spreadsheets using AI prompts.

---

## The problem

You've just finished an experiment. You have:
- qPCR data from 384-well plate (Cq values in a weird format)
- Plate reader output (Excel file with merged cells)
- Manually entered observations (typos, inconsistent units)
- Microscopy counts (different people, different conventions)

You need to:
1. Clean the data (remove obvious errors, standardize units)
2. Normalize (to controls, to housekeeping genes)
3. Calculate derived values (fold change, % viability, etc.)
4. Format for statistics software

This usually takes **hours of manual Excel work**. AI can compress this to **minutes** — if you prompt it correctly.

---

## 🎯 What you'll learn

1. The 4-step data cleaning workflow
2. How to write data-cleaning prompts that work
3. When to trust AI's cleanup vs when to verify manually
4. How to handle common biology data formats (qPCR, plate readers, microscopy)
5. India-specific: dealing with data from instruments using regional software (often Hindi/regional language labels)

---

## 📊 The 4-step data cleaning workflow

### Step 1: Inspect the raw data (5 min)

Before any AI, open the file and:
- Count rows + columns
- Note the format (CSV, XLSX, TSV)
- Identify any merged cells, blank rows, weird headers
- Check units (ng/μL vs ng/mL vs mg/mL)
- Check date format (DD/MM/YYYY vs MM/DD/YYYY — Indian labs use both!)

**Don't skip this.** AI can't see what you don't tell it.

### Step 2: Describe the data to AI (5 min)

Use this prompt template:

```
I have experimental data from a [experiment type]. 
Please help me clean it.

Data format: [CSV/XLSX/TSV]
Rows: [number]
Columns: [list column names]
Units: [list units per column]
Known issues: [typos, missing values, outliers, etc.]

Goal: [what you want at the end — normalized values, fold change, etc.]

[Attach the file or paste sample]
```

### Step 3: Apply AI suggestions (10 min)

AI will give you:
- Cleanup steps (Python or R code, or Excel formulas)
- Format recommendations
- Outlier detection suggestions

**Apply these one at a time and verify each.**

### Step 4: Verify the cleaned data (5 min)

Before exporting for analysis:
- [ ] Compare 5 random raw values vs cleaned values (did AI change them correctly?)
- [ ] Check totals (does cleaned data sum to what raw data summed to?)
- [ ] Check units consistency
- [ ] Save a copy of raw data BEFORE any changes

---

## 🔧 Common biology data formats + AI prompts

### 1. qPCR data (Cq values)

**Raw data looks like:**
| Well | Sample | Cq | Target |
|------|--------|----|--------|
| A1 | S1 | 18.4 | GAPDH |
| A2 | S1 | 18.6 | GAPDH |
| A3 | S1 | 24.1 | GeneX |
| A4 | S2 | 18.3 | GAPDH |
| A5 | S2 | 18.5 | GAPDH |
| A6 | S2 | 25.8 | GeneX |

**Cleaning needed:**
- Remove wells with Cq > 35 (unreliable)
- Remove wells with SD > 0.5 between technical replicates
- Calculate ΔCq = Cq(target) - Cq(GAPDH)
- Calculate ΔΔCq = ΔCq(sample) - ΔCq(control)
- Calculate fold change = 2^(-ΔΔCq)

**AI prompt that works:**

```
I have qPCR data from a 96-well plate. Each sample has 3 technical replicates 
for GAPDH (housekeeping) and 3 for my gene of interest.

Attached: qPCR_data.csv

Please:
1. Calculate mean Cq and SD for each technical replicate group
2. Flag any wells where SD > 0.5 (unreliable)
3. Flag any Cq > 35 (unreliable)
4. Calculate ΔCq = Cq_target - Cq_GAPDH per sample
5. Calculate ΔΔCq = ΔCq_sample - mean(ΔCq_control)
6. Calculate fold change = 2^(-ΔΔCq)

Output as a new CSV with columns: Sample, Treatment, Mean_Cq_target, 
Mean_Cq_GAPDH, ΔCq, ΔΔCq, Fold_Change, QC_Flag
```

**AI gotcha:** It may suggest using **18S rRNA** instead of GAPDH if your cell type isn't standard. Verify your housekeeping gene choice for your cell type.

---

### 2. Plate reader output (OD, fluorescence)

**Raw data from a plate reader** is usually:
- Wide format (96-well plate layout: A1-H12 rows, 1-12 columns)
- Multiple time points (kinetic reads)
- Units in arbitrary "RFU" or "OD"

**Cleaning needed:**
- Subtract blank (media only wells)
- Calculate mean + SD of technical replicates
- Time-course normalization (baseline = time 0)

**AI prompt:**

```
I have plate reader data from an MTT assay. 96-well plate, 4 conditions 
(Control, Drug A, Drug B, Drug C), 6 replicates each, 24-hour time course.

Attached: mtt_data.csv (wide format, rows = time points, columns = wells)

The plate layout is:
- Column 1-6: Control
- Column 7-12: Drug A 10μM
- ... etc

Please:
1. Reshape to long format: Time, Condition, Well, OD
2. Subtract blank (mean of A1-A6 which are media-only)
3. Calculate mean + SD per condition per time point
4. Normalize to t=0 per condition (% viability vs t=0)
5. Output as: Time, Condition, Mean_OD, SD, Pct_Viability
```

---

### 3. Microscopy cell counts

**Common issue:** Different lab members count with different conventions.
- Person A: "TNC" (total nucleated cells)
- Person B: "live cells only"
- Person C: includes debris

**AI prompt:**

```
I have manual cell counts from a hemocytometer. Different lab members 
entered data with inconsistent labeling.

Attached: cell_counts.csv

Please:
1. Standardize column names (currently mixed: "count", "Cell Count", "n_cells")
2. Convert all counts to cells/mL using hemocytometer formula 
   (count × 10^4 / dilution_factor)
3. Flag any counts with viability < 70% (suspicious)
4. Calculate mean + SD per condition per replicate
5. Output clean long format
```

---

### 4. Western blot densitometry

**Common tools:** ImageJ / Fiji for band quantification

**Cleaning needed:**
- Subtract background
- Normalize to loading control (β-actin, GAPDH, vinculin)
- Calculate fold change vs control

**AI prompt:**

```
I have ImageJ densitometry output from Western blots. Each blot has:
- Target protein band (variable)
- Loading control band (β-actin)

Attached: densitometry.csv with columns: Blot_ID, Sample, Treatment, 
Target_Intensity, Loading_Control_Intensity

Please:
1. Calculate ratio = Target / Loading_Control per sample
2. Normalize each blot to its control sample (Control = 1.0)
3. Flag any samples where Loading_Control is < 10% of blot mean 
   (loading issue)
4. Calculate mean + SD per treatment
5. Output as: Sample, Treatment, Normalized_Expression, QC_Flag
```

---

## 🚨 When AI gets data cleaning WRONG

### Common errors

1. **Wrong date parsing** — "01/02/2024" could be Jan 2 or Feb 1. AI may guess wrong.
   - **Fix:** Always specify date format in your prompt
   
2. **Wrong unit conversion** — ng/μL vs ng/mL confusion. 1000× error.
   - **Fix:** Always state units explicitly. Verify AI's conversions.

3. **Wrong decimal separator** — Indian data often uses comma (1,23,456.78). AI may break.
   - **Fix:** Convert to international format (123456.78) before AI processing.

4. **Wrong handling of "below detection limit"** — Often coded as "ND", "<0.01", "BQL", "0", or left blank.
   - **Fix:** Tell AI how to handle these explicitly.

5. **Merged cells in Excel** — AI may miss these if parsing raw text.
   - **Fix:** Unmerge cells before uploading, or use openpyxl/pandas.

6. **Hindi/regional column headers** — Some Indian labs use bilingual labels.
   - **Fix:** Standardize to English headers before AI.

### Case study: Real Indian lab data error

A research group used AI to "clean" their ELISA data. The plate had blank wells (media only) in column 1 and serial dilutions of standard in columns 2-12. AI subtracted column 1 mean from everything — **including the standards themselves.** Result: standard curve was wrong, all concentrations were 30% off.

**Lesson:** Verify AI's blank subtraction logic against the plate layout.

---

## ✅ The verification checklist (always do this)

Before exporting cleaned data for stats:

- [ ] **Pick 5 random raw values.** Manually compute what the cleaned value should be. Compare to AI's output.
- [ ] **Check totals.** If raw data summed to 1000, cleaned data should too (or close).
- [ ] **Check units.** Look at 3 random values, confirm units are correct.
- [ ] **Check for false positives.** Did AI "fix" something that wasn't broken?
- [ ] **Save raw data separately.** Never overwrite original.

**Time for verification:** 5-10 minutes. Saves hours of debugging later.

---

## 🎯 Hands-on demo

In the video, I demonstrate cleaning 3 messy datasets:

**Dataset 1:** qPCR plate with mixed notation, some wells with no Cq, others with weird symbols
**Dataset 2:** Plate reader MTT assay with 24-hour time course, 4 conditions
**Dataset 3:** Western blot densitometry from 3 different blots, inconsistent loading controls

**Result:** All 3 datasets cleaned in 12 minutes total (vs ~2 hours manual).

**Watch:** [Video timestamp 28:30]

---

## 🎯 Action items

Before moving to Lesson 3.2:

- [ ] Pick one of YOUR messy datasets (any biology data you have)
- [ ] Write an AI prompt using the templates above
- [ ] Apply AI's suggestions to your data
- [ ] Verify 5 random values manually
- [ ] Save cleaned data + raw data separately

---

## 📚 Additional resources

- **AlterLab skills used:**
  - `alterlab-data-analysis` — general data wrangling
  - `alterlab-spreadsheet-intelligence` — Excel/Sheets automation
  - `alterlab-statistics` — when you get to Lesson 3.2
- **Tools tutorials:**
  - **OpenRefine** (free) — open-source data cleaning, great for messy CSVs
  - **pandas** (Python) — if you'll do this repeatedly, learn pandas
  - **tidyverse** (R) — same for R users
- **India-specific:**
  - **NumPy/pandas in Hindi tutorials** — YouTube has growing Hindi data science content
  - **InSTI (Indian Statistical Institute)** — offers short courses on data analysis

---

## ⚠️ Common mistakes

### Mistake 1: Letting AI change raw data
Always save a copy of raw data. AI should produce NEW columns or NEW files, not modify originals.

### Mistake 2: Not specifying units
"100" of what? ng? μg? cells/mL? Always specify.

### Mistake 3: Trusting outlier detection blindly
AI may flag biologically meaningful outliers as "errors." Verify each flag.

### Mistake 4: Skipping the inspect step
You need to know what your data looks like before AI can help.

### Mistake 5: Not handling missing data explicitly
What should AI do with empty cells? Skip? Treat as 0? Impute? Specify.

---

**Next lesson:** [Lesson 3.2 — Statistics Without Tears](./02-statistics-without-tears.md) →