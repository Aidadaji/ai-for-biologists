# Lesson 3.4 — Interpreting AI Analysis

**Duration:** 60 minutes
**Video:** [Link]
**Outcome:** Sanity-check AI's interpretation of your data, build intuition for when AI is right vs wrong, and develop your own analytical judgment.

---

## The problem

You have your data, you ran the analysis, and AI gave you an interpretation:
> "These results suggest that Drug X significantly inhibits cell growth through apoptosis induction, consistent with its known role as a p53 activator..."

But is this right? Is it what your data actually shows? Or is AI making things up?

This lesson teaches you to **think critically** about AI interpretations.

---

## 🎯 What you'll learn

1. The 4 types of AI interpretation errors
2. The "sanity check" framework for any AI interpretation
3. How to build your own interpretation skills (not just trust AI)
4. When to override AI with your domain expertise
5. How to write the discussion section based on YOUR interpretation (not AI's)

---

## 🧠 The 4 types of AI interpretation errors

### Error 1: Over-claiming
**AI loves to write:** "This demonstrates that..." / "This proves..."

**Reality:** Your data probably "suggests" or "indicates," not "demonstrates."

**Example:**
- AI: "This demonstrates that Drug X induces apoptosis via caspase-3 activation."
- Reality: Your data shows increased caspase-3 activity. You haven't shown it's the CAUSE of apoptosis (could be a consequence, parallel event, or unrelated).

**Fix:** Replace "demonstrates" with "suggests" or "is consistent with."

### Error 2: Wrong mechanism
**AI guesses mechanisms** based on its training data, not your data.

**Example:**
- Your data: Drug X reduces cell viability by 50%
- AI: "This is likely via apoptosis induction based on published literature."
- Reality: Could be apoptosis, necrosis, senescence, autophagy, cell cycle arrest, or off-target toxicity.

**Fix:** Don't claim mechanism without measuring it directly. Use language like "We hypothesize that..." or "Further studies are needed to determine..."

### Error 3: Cherry-picked literature
**AI selectively cites papers** that support your finding.

**Reality:** There may be contradicting papers AI didn't mention.

**Fix:** 
- Ask AI: "Are there contradicting studies? What's the controversy?"
- Search Google Scholar yourself for contradicting evidence
- Read 2-3 review articles to understand the debate

### Error 4: Conflating correlation with causation
**AI doesn't distinguish** between correlation and causation in biology.

**Example:**
- Your data: Cells with high Drug X also have low viability
- AI: "Drug X causes viability reduction."
- Reality: Drug X CORRELATES with low viability. Could be that Drug X has off-target effects, the cells were already dying, etc.

**Fix:** Use careful language: "associated with" not "caused."

---

## ✅ The sanity check framework

Before accepting any AI interpretation, run it through this 5-question framework:

### Q1: Does the interpretation match my data?

**Self-check:** Read AI's interpretation. Does each claim correspond to something you actually measured?

**Example:**
- AI: "Drug X reduced viability to 50% of control (p<0.001)"
- Your data: Mean viability = 50% of control, p=0.0008 from t-test
- ✅ AI's claim matches your data

**Example of mismatch:**
- AI: "Drug X reduced viability to 50%"
- Your data: Actually 65% of control
- 🚨 AI hallucinated the number

### Q2: Does the interpretation make biological sense?

**Self-check:** Apply your domain knowledge. Is this biologically plausible?

**Example:**
- AI: "Drug X (a kinase inhibitor) reduced viability by activating caspase-3"
- Biological sense: Kinase inhibitors CAN trigger apoptosis. Plausible.
- ✅ No red flag

**Example of red flag:**
- AI: "Drug X (a transcription factor) reduced viability by activating caspase-3"
- Biological sense: Transcription factors don't directly activate caspases. Suspicious.
- 🚨 Question this claim

### Q3: Is the mechanism claim justified by YOUR data?

**Self-check:** If AI claims a mechanism, did you measure that mechanism?

**Example:**
- AI: "Viability reduction is via apoptosis"
- Your data: You measured viability (MTT assay) but not apoptosis
- 🚨 Cannot claim apoptosis. Can only say "consistent with" apoptosis.

**Fix:** Use "may involve" or "is consistent with" if you didn't measure the mechanism.

### Q4: Is the comparison fair?

**Self-check:** Are you comparing the right controls?

**Example:**
- AI: "Drug X reduced viability vs no treatment"
- Reality: You compared to DMSO control (not "no treatment")
- 🚨 AI misrepresented the control

**Fix:** Specify the actual controls in the interpretation.

### Q5: Does the conclusion match the evidence strength?

**Self-check:** Are you/AI over-claiming given your sample size, study design, etc.?

**Example:**
- AI: "Drug X is a potent inhibitor of cell growth"
- Your data: n=3 per group, p<0.05, single experiment
- Reality: Can't claim "potent" from one experiment with n=3.

**Fix:** Tone down to "In our preliminary data, Drug X reduced viability..."

---

## 🧪 Hands-on examples: AI right vs AI wrong

### Example 1: AI is right

**Data:** qPCR shows 5-fold increase in Bax gene expression after Drug X treatment.

**AI interpretation:** "These results suggest that Drug X treatment upregulates the pro-apoptotic gene Bax, consistent with activation of the intrinsic apoptotic pathway."

**Sanity check:**
- Q1: Does it match data? ✅ (5-fold = "upregulation")
- Q2: Biologically plausible? ✅ (Bax is pro-apoptotic)
- Q3: Mechanism justified? ⚠️ (AI says "intrinsic apoptotic pathway" but you didn't measure other intrinsic pathway components)
- Q4: Comparison fair? ✅ (treated vs untreated control)
- Q5: Evidence strength? ⚠️ (n=? mentioned? Single gene ≠ full pathway)

**Verdict:** Mostly right, but tone down the pathway claim. Say "upregulates Bax, suggesting possible involvement of apoptotic pathways."

---

### Example 2: AI is wrong

**Data:** MTT assay shows 30% reduction in viability with Drug X.

**AI interpretation:** "These results demonstrate that Drug X induces apoptosis via the mitochondrial pathway, as evidenced by reduced viability."

**Sanity check:**
- Q1: Does it match data? ⚠️ (30% reduction, not "demonstrates")
- Q2: Biologically plausible? ✅ (plausible mechanism)
- Q3: Mechanism justified? 🚨 (You measured viability, NOT apoptosis or mitochondrial pathway)
- Q4: Comparison fair? ✅ (treated vs control)
- Q5: Evidence strength? 🚨 (MTT alone cannot establish mechanism)

**Verdict:** AI over-claimed. You measured viability reduction, not apoptosis. Revise to: "Drug X reduces viability. Further studies (caspase-3 assay, annexin V staining) are needed to determine if apoptosis is involved."

---

### Example 3: AI makes something up

**Data:** Cell counts show Drug X reduces proliferation.

**AI interpretation:** "Drug X (a known p53 activator, per Smith et al. 2018) reduced proliferation by 40%, consistent with p53-mediated cell cycle arrest."

**Sanity check:**
- Q1: Does it match data? ✅ (40% reduction in counts)
- Q2: Biologically plausible? ✅
- Q3: Mechanism justified? 🚨 (You measured counts, not p53 or cell cycle)
- Q4: Comparison fair? ✅
- Q5: Evidence strength? 🚨 (citing Smith et al. without verification = possible fabrication)

**Verdict:** Multiple issues. AI invented the "Smith et al. 2018" citation (verify it!). Even if it exists, citing it doesn't prove Drug X works via p53 in YOUR system. Revise to just describe your data + suggest future experiments.

---

## 🛠️ Building your own interpretation skills

The best defense against AI misinterpretation is **strong domain knowledge**.

### Exercise 1: The "blind interpretation" test

**Try this:** Look at a figure from a paper. Write your interpretation in 100 words. Then read the paper's interpretation. Compare.

What did you catch that AI missed? What did AI add that you missed?

### Exercise 2: The "5-year-old test"

Explain your data to a 5-year-old. If you can't, you don't really understand it.

> "We put some cells in a dish and added a drug. After 3 days, less cells were alive. Maybe the drug hurt them, but we don't know exactly how."

If AI's interpretation can't be reduced to this level, it's probably over-claiming.

### Exercise 3: The "publication test"

Imagine your most critical reviewer reading your interpretation. What would they object to?

If AI's interpretation uses phrases that would get a reviewer angry ("definitively shows," "proves," "demonstrates without doubt"), revise them.

### Exercise 4: The "alternative explanations" test

For every interpretation, list 3 alternative explanations:

- "Drug X reduces viability."
- Alternative 1: Cells died from old age / over-confluence
- Alternative 2: Drug precipitated in media, reducing nutrients
- Alternative 3: Off-target toxicity

If you can't list alternatives, you're probably over-confident.

---

## 🇮🇳 India-specific interpretation pitfalls

### 1. Batch effects misread as treatment effects
Indian labs may run experiments across multiple batches (different days, different reagent lots). A "treatment effect" might actually be a batch effect.

**Fix:** Include batch as a covariate in your analysis. Plot data colored by batch.

### 2. Seasonal variation
Some biological processes vary by season in India (circadian, immune function, plant growth cycles). A "treatment effect" might be seasonal.

**Fix:** Replicate experiments across seasons if claiming a robust effect.

### 3. Genetic diversity in Indian populations
If using cell lines from Indian donors (e.g., cord blood), genetic diversity is higher than typical lab lines. "Outliers" may actually be normal variation.

**Fix:** Increase sample size. Verify "outliers" by checking the raw data.

### 4. Crowded lab conditions
Indian labs are often more crowded. Temperature, humidity, vibration can vary. Affects sensitive assays (qPCR, microscopy).

**Fix:** Log environmental conditions. Include as covariates if needed.

---

## 📝 Writing your own interpretation (the right way)

### Template: From data to discussion

**Step 1: Describe what you observed (no interpretation)**

> "Drug X reduced cell viability to 50% of control at 10 μM after 72 hours (Figure 1A). This effect was dose-dependent (Figure 1B)."

**Step 2: Compare to literature**

> "This is consistent with Smith et al. (2019) who reported 60% reduction with Drug X in similar conditions, though at higher dose (50 μM)."

**Step 3: Suggest mechanism (hedged)**

> "The reduction in viability may involve apoptosis, as Drug X has been shown to activate caspase-3 in other cell types (Jones et al., 2020). However, we did not directly measure apoptosis in this study."

**Step 4: Acknowledge limitations**

> "This experiment was performed with n=3 per condition in a single experiment. Replication and additional assays (annexin V, caspase-3) are needed to confirm these findings."

**Step 5: Future directions**

> "Future studies should investigate the mechanism of Drug X-induced viability reduction and determine whether this effect is observed in primary cells or in vivo."

**Notice:** No "demonstrates," no "proves," no over-claiming.

---

## ✅ The "before AI" checklist

Before you ask AI to interpret your data, do this yourself first:

- [ ] Make your own plot (does it look like what you expected?)
- [ ] Calculate basic stats yourself (mean, SD, p-value)
- [ ] Write your interpretation in 100 words
- [ ] List 3 alternative explanations for your observation
- [ ] Find 1-2 relevant papers in literature
- [ ] Note any limitations or caveats

**THEN** ask AI to:
- Refine your interpretation (not replace it)
- Suggest alternative explanations you missed
- Find additional relevant literature
- Check for over-claiming language

---

## 🤖 Good AI prompts for interpretation

### Prompt 1: Refine my interpretation (don't replace)

```
I have data from a [experiment type]. Here's my draft interpretation:

"[your 100-word interpretation]"

Please:
1. Identify any over-claiming language
2. Suggest revisions for more appropriate hedging
3. Add any biological mechanisms I should mention (with citations to verify)
4. Note any limitations I missed

DO NOT replace my interpretation — just refine it. I will verify all citations.
```

### Prompt 2: Find contradicting studies

```
I observed [your observation]. The typical interpretation is [common interpretation].

Please:
1. Are there contradicting studies?
2. What's the current debate in the field?
3. Are there alternative explanations I should consider?

I will verify each citation you provide.
```

### Prompt 3: Sanity check my interpretation

```
I concluded that [your conclusion]. Is this:
1. Supported by the data I described?
2. Biologically plausible?
3. Appropriately hedged (not over-claiming)?
4. Consistent with the current literature?

Suggest revisions if needed.
```

---

## 🎯 Hands-on demo

In the video, I demonstrate:
1. AI interpretation of real biology data (3 examples)
2. Running the 5-question sanity check
3. Revising over-claimed interpretations
4. Adding limitations and future directions
5. Writing a publication-ready discussion section

**Watch:** [Video timestamp 27:00]

---

## 🎯 Action items

Before starting Module 3 labs:

- [ ] Take a figure from your own work (or a published paper)
- [ ] Write a 100-word interpretation WITHOUT AI
- [ ] Ask AI to interpret the same figure
- [ ] Compare your interpretation vs AI's
- [ ] Run sanity check (5 questions)
- [ ] Identify AI's errors + revise
- [ ] Write a publication-ready version

---

## 📚 Additional resources

- **AlterLab skills used:**
  - `alterlab-paper-reviewer` — critical paper review (including over-claim detection)
  - `alterlab-scientific-writing` — appropriate hedging language
  - `alterlab-bias-detection` — finding AI's interpretive biases
- **Papers on over-claiming in biology:**
  - "The natural selection of bad science" (Smaldino & McElreath, 2016)
  - "Statistical errors in biology" (many examples)
- **Indian resources:**
  - **Indian Academy of Sciences** — publishes discussion of methodological standards
  - **Current Science** — has editorials on common interpretation errors

---

## ⚠️ Common mistakes

### Mistake 1: Using AI's interpretation as your own
Always revise AI's interpretation in your own words. Submitting AI text verbatim is academic misconduct.

### Mistake 2: Accepting "consistent with literature" without checking
If AI says "consistent with Smith et al. 2019," verify Smith et al. 2019 actually exists AND actually supports your claim.

### Mistake 3: Letting AI choose which papers to cite
AI may cite only papers that support your hypothesis. Search independently for contradicting evidence.

### Mistake 4: Using "demonstrates" for correlation studies
"X correlates with Y" ≠ "X demonstrates X causes Z."

### Mistake 5: Not acknowledging limitations
Every study has limitations. Pretending they don't exist = reviewer red flag.

### Mistake 6: Over-interpreting preliminary data
If you have n=3 from one experiment, you have preliminary data, not definitive evidence.

---

**Next:** [Module 3 Labs →](./labs/)