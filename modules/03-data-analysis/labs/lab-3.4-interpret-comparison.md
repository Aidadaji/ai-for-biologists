# Lab 3.4 — Compare AI vs Human Data Interpretation

**Time:** 75 minutes
**Difficulty:** 🟡 Medium
**Tools:** Claude (or ChatGPT), Google Sheets (or notebook)

---

## 🎯 Objective

For 3 real biology datasets, write your OWN interpretation first, then ask AI for its interpretation. Compare. Identify where AI over-claims, fabricates, or misses nuances.

This is the most important lab for building **your critical thinking** vs AI dependency.

---

## 📋 What you'll submit

1. **Your interpretations** — written before AI for each dataset (100 words each)
2. **AI interpretations** — what AI said for each dataset
3. **Comparison table** — where you and AI agree, where you disagree
4. **Critical analysis** — 3 cases where AI was wrong, 3 cases where AI added value
5. **Reflection** — what you learned about AI's strengths and weaknesses

---

## 📊 The 3 datasets (provided)

### Dataset A: Drug X + cell viability (MTT assay)

You're testing Drug X (a novel kinase inhibitor) on cancer cell viability.

**Data:**
| Condition | Replicate | Viability (% control) |
|-----------|-----------|----------------------:|
| Control (DMSO) | 1 | 100 |
| Control (DMSO) | 2 | 98 |
| Control (DMSO) | 3 | 102 |
| Drug X 1μM | 1 | 95 |
| Drug X 1μM | 2 | 92 |
| Drug X 1μM | 3 | 97 |
| Drug X 10μM | 1 | 65 |
| Drug X 10μM | 2 | 68 |
| Drug X 10μM | 3 | 63 |
| Drug X 100μM | 1 | 25 |
| Drug X 100μM | 2 | 22 |
| Drug X 100μM | 3 | 28 |

**Quick stats (do this first yourself):**
- Control mean = 100, SD ≈ 2
- Drug 1μM mean = 94.7, SD ≈ 2.5
- Drug 10μM mean = 65.3, SD ≈ 2.5
- Drug 100μM mean = 25, SD ≈ 3

One-way ANOVA + Tukey: p<0.001 across groups

---

### Dataset B: Protein expression (Western blot)

You're measuring BCL2 protein levels in tumor vs normal tissue.

**Data:**
| Sample | Tissue | BCL2/β-actin ratio |
|--------|--------|-------------------:|
| 1 | Normal | 0.85 |
| 2 | Normal | 0.92 |
| 3 | Normal | 0.88 |
| 4 | Tumor | 1.45 |
| 5 | Tumor | 1.52 |
| 6 | Tumor | 1.38 |
| 7 | Tumor | 2.10 |
| 8 | Tumor | 2.05 |
| 9 | Tumor | 1.95 |

(Wait — sample 7-9 look like they might be from a different subgroup!)

---

### Dataset C: Cell migration assay

You're testing if Growth Factor Y promotes cell migration.

**Data:**
| Condition | Migrated cells (per field) |
|-----------|---------------------------:|
| Control | 12 |
| Control | 15 |
| Control | 10 |
| Control | 13 |
| Growth Factor Y | 45 |
| Growth Factor Y | 48 |
| Growth Factor Y | 42 |
| Growth Factor Y | 50 |

**Quick stats:**
- Control mean = 12.5
- Growth Factor Y mean = 46.25
- Independent t-test: p<0.001 (highly significant)

---

## 📝 Step-by-step instructions

### Step 1: Write YOUR interpretation first (20 min)

For each dataset, write a 100-word interpretation. **No AI yet.**

**Template:**

```markdown
## Dataset A interpretation

### What I observed:
[Describe what the data shows in plain language]

### Statistical result:
[Test used, p-value, effect size]

### What I think it means:
[Biological interpretation, with appropriate hedging]

### Limitations:
[What this study CAN'T tell us]

### Next experiments:
[What would I do next to confirm/extend?]
```

**Example for Dataset A (your version will differ):**

> Drug X reduces cell viability in a dose-dependent manner. The effect is significant at 10μM (~35% reduction) and 100μM (~75% reduction), but minimal at 1μM (~5% reduction). The dose-response suggests a specific effect, not general toxicity (which would show effects at all doses). However, this is only an MTT assay — I haven't measured apoptosis, necrosis, or cell cycle arrest. The mechanism is unknown. I'd need caspase-3 assays, Annexin V staining, and possibly target engagement confirmation (phospho-specific Western blot for the kinase target) to understand HOW Drug X is working.

---

### Step 2: Ask AI for its interpretation (10 min)

**Prompt template:**

```
I have a biology dataset. Please write a 100-word interpretation.

Dataset: [describe data, paste table]

Context: [what experiment, what cell type, what you're testing]

Please include:
1. What the data shows
2. Statistical interpretation (just describe, don't re-analyze)
3. Biological meaning
4. Limitations
5. Suggested next experiments

Be careful to:
- Not over-claim mechanism (I only measured viability, not mechanism)
- Use appropriate hedging language
- Acknowledge what the data can't tell us
```

**Run for each dataset.**

---

### Step 3: Compare your interpretation vs AI's (15 min)

Create a comparison table:

```markdown
## Dataset A comparison

| Aspect | My interpretation | AI's interpretation | Agree? |
|--------|-------------------|--------------------|--------|
| Dose-dependent? | Yes | ? | ? |
| Significant? | Yes (10, 100μM) | ? | ? |
| Mechanism claim | None (only measured viability) | ? | ? |
| Limitations | Yes (MTT only) | ? | ? |
| Next experiments | 3 specific | ? | ? |
| Over-claiming? | No | ? | ? |
```

---

### Step 4: Critical analysis — when AI was wrong (15 min)

For each dataset, identify any AI errors:

**Common AI errors to look for:**

1. **Over-claiming mechanism** — AI says "Drug X induces apoptosis via caspase-3" when you only measured viability
2. **Wrong statistics** — AI says "p<0.001" but doesn't specify the test
3. **Fabricated literature** — AI cites "Smith et al. 2019" that doesn't exist
4. **Missing limitations** — AI doesn't acknowledge what wasn't measured
5. **Wrong generalization** — AI says "this means Drug X works in all cancers"
6. **Confusing correlation with causation** — AI implies Drug X causes viability reduction in patients (you tested cells in vitro)
7. **Cherry-picked controls** — AI doesn't mention that you only compared to DMSO, not to a no-treatment control

**For each error you find, write:**

```markdown
### Error 1: Over-claiming mechanism

**AI said:** "Drug X reduces viability by inducing apoptosis."

**Why this is wrong:**
I only measured viability (MTT assay). Apoptosis is one possible mechanism, but I haven't measured:
- Caspase-3 activation
- Annexin V staining
- DNA fragmentation
- Morphological changes

**Correct interpretation:** "Drug X reduces viability. The mechanism is unknown and requires further investigation."

**Lesson:** AI extrapolates beyond the data. Always check if claims are justified by what was actually measured.
```

---

### Step 5: Critical analysis — when AI added value (10 min)

For each dataset, also identify where AI's interpretation was helpful:

- **Found literature you missed** — AI cited a paper you hadn't thought of
- **Better biological framing** — AI explained mechanism more clearly
- **Caught limitations you missed** — AI noted something you hadn't considered
- **Suggested experiments you didn't think of** — AI's ideas expanded your next-steps list

---

### Step 6: Reflection (5 min)

Write a 200-word reflection:

```markdown
## Reflection

### What I learned about AI interpretation:

1. [Lesson 1]
2. [Lesson 2]
3. [Lesson 3]

### When I trust AI more:
[Scenarios where AI's interpretation was reliable]

### When I trust AI less:
[Scenarios where AI's interpretation was unreliable]

### How I'll use AI going forward:
[Will you use AI for interpretation? How?]
```

---

## ✅ Success criteria

You pass this lab if:
- [ ] Your interpretations written BEFORE AI (not after)
- [ ] Comparison table completed for all 3 datasets
- [ ] At least 3 AI errors identified with corrections
- [ ] At least 3 cases where AI added value
- [ ] Reflection is honest and specific

---

## 🚨 Common AI interpretation errors (what to look for)

### Error type 1: Mechanism over-claim
**AI:** "Drug X induces apoptosis via caspase-3 activation."
**Reality:** Only measured viability. No apoptosis data.

### Error type 2: Generalization
**AI:** "This drug could be effective for treating cancer in patients."
**Reality:** Tested cancer cells in vitro. Animal/human data not available.

### Error type 3: Missing subgroup
**AI (Dataset B):** "BCL2 is upregulated in tumor tissue."
**Reality:** Tumor samples 7-9 might be a different subgroup (higher BCL2). AI missed this pattern.

### Error type 4: Confusing correlation with causation
**AI (Dataset C):** "Growth Factor Y promotes cell migration, suggesting it could enhance metastasis in cancer patients."
**Reality:** Migration in vitro ≠ metastasis in patients. Many steps in between.

### Error type 5: Cherry-picked comparison
**AI:** "Drug X is effective at 10μM."
**Reality:** "Effective" compared to what? vs DMSO control only. Not vs other drugs.

### Error type 6: Statistical over-claim
**AI:** "These results are highly significant and conclusive."
**Reality:** n=3 per group, single experiment. p<0.05 ≠ conclusive.

### Error type 7: Fabricated citation
**AI:** "Consistent with Smith et al. (2019) who showed..."
**Reality:** Verify Smith et al. 2019 exists + actually supports the claim.

---

## 🇮🇳 India-specific interpretation pitfalls

### Sample B: Tumor vs normal
Indian tumor samples often come from heterogeneous sources (different hospitals, different stages). The 3 "high BCL2" samples (7-9) might be:
- From a specific cancer subtype
- From later-stage tumors
- From a different organ
- Different storage conditions

**Real interpretation:** "BCL2 is elevated in tumor vs normal tissue. However, the 3 highest samples (7-9) may represent a distinct subgroup. Further characterization (cancer subtype, stage, etc.) needed."

### Sample C: Migration assay
Indian labs often run these assays with:
- Different cell passage numbers
- Different serum batches
- Different time points
- Variable wound widths (if scratch assay)

**Real interpretation:** "Growth Factor Y increased migration 3.7-fold under our specific conditions. Whether this is reproducible across passages, serum batches, and time points requires further validation."

---

## 📊 Sample comparison (Dataset A)

| Aspect | Your version | AI version (typical) | Agree? |
|--------|--------------|---------------------|--------|
| Dose-dependent | Yes | Yes | ✅ |
| Significant at 10, 100μM | Yes | Yes | ✅ |
| **Mechanism** | "Unknown, needs apoptosis assays" | "Via apoptosis induction" | ❌ AI over-claims |
| **Generalization** | "In MTT assay" | "Effective in cancer cells" | ⚠️ AI too broad |
| **Limitations** | MTT only, n=3, single expt | "n is small" | ⚠️ AI missed key limitations |
| **Next experiments** | Caspase-3, Annexin V, target engagement | "Western blot" | ⚠️ AI vague |
| **Over-claiming?** | No | Yes | ❌ AI |

**Lesson:** AI sounds confident but extrapolates beyond the data. Your interpretation (with appropriate hedging) is more scientifically accurate.

---

## 🚀 Stretch goals

### Stretch 1: Try multiple AI tools
Ask Claude, ChatGPT, and Gemini the same questions. Compare interpretations. Which is most accurate?

### Stretch 2: Adversarial interpretation
Give AI a deliberately problematic dataset (e.g., with outliers or confounders). Does AI catch the issues?

### Stretch 3: Domain expert comparison
Find a published paper with a similar experiment. Compare the published interpretation to yours and AI's. Which is closest to published?

### Stretch 4: Build your own checklist
Based on what you learned, write a 10-item checklist for evaluating AI interpretations. Use it in your future research.

---

## ❓ Troubleshooting

**Q: AI gave a very different interpretation than mine. Who's right?**
A: Apply the sanity check (Q1-Q5 from Lesson 3.4). Whichever interpretation is better supported by the actual data is more accurate.

**Q: My interpretation was wrong / AI was right on something. Is that bad?**
A: No — that's a learning opportunity. Note it in your reflection. Adjust your interpretation process.

**Q: AI's interpretation is more "polished" than mine. Should I use AI's?**
A: Polished ≠ accurate. Your interpretation may be rougher but more scientifically honest. Always prioritize accuracy.

**Q: What if AI caught something I missed (a limitation, an alternative interpretation)?**
A: That's exactly what AI should be used for — augmenting YOUR thinking, not replacing it. Note it in your "AI added value" section.

---

## 📚 What's next

→ **[Module 4: AI for Scientific Writing →](../04-scientific-writing/README.md)**

In Module 4, you'll learn to write manuscripts using AI while maintaining scientific integrity.

---

**Time check:** If you took more than 90 min, that's OK. Critical thinking is hard and worth the time.

---

## 🎓 Final thought

**The best biologists of the AI era won't be those who use AI the most — they'll be those who use AI the most critically.**

This lab trains that critical muscle. Use it on every AI interpretation you encounter for the rest of your career.