# Lab 1.3 — Catch 5 Hallucinations in AI-Generated Summaries ⚠️

**Time:** 75 minutes
**Difficulty:** 🟡 Medium
**Tools:** Claude (or ChatGPT), Google Scholar, PubMed, UniProt, NCBI

---

## ⚠️ Why this lab is CRITICAL

LLMs confidently fabricate things that don't exist. In biology, this means:
- Citing papers that were never published
- Quoting statistics from studies that don't exist
- Misattributing discoveries to wrong authors
- Inventing gene names that look real

**If you submit AI-generated content without verification, your paper will be flagged by reviewers.** Worse, you might embarrass yourself in a viva or presentation.

This lab trains your verification reflexes.

---

## 🎯 Objective

Given 5 AI-generated biology summaries (provided below), identify and document the hallucination in each.

---

## 📋 What you'll submit

A Google Doc or Markdown file with:
- 5 AI summaries (provided)
- Your "hallucination catch log" — for each summary, document:
  - **Claim type:** What was fabricated? (DOI, gene name, statistic, etc.)
  - **Verification method:** How did you catch it?
  - **Authoritative source:** Link/citation to the correct information
  - **Time taken:** How long did verification take?

---

## 📝 The 5 AI-generated summaries (with planted errors)

**Important:** Read these as if a colleague or AI tool gave them to you. **Do not assume they're correct.** Some are accurate; some contain hallucinations.

---

### Summary 1: Cancer immunotherapy review

> **Claim:** "CRISPR-Cas9 was first used in a clinical trial for cancer in 2016 by the University of Pennsylvania, led by Dr. Edward Stadtmauer (Nature, 2019, DOI: 10.1038/s41586-019-0944-6). The trial showed complete remission in 60% of patients with refractory B-cell malignancies."

**Your task:** Verify this claim. Check:
- [ ] DOI exists
- [ ] First author and journal correct
- [ ] The 60% remission statistic
- [ ] Whether this was actually the first CRISPR cancer trial

---

### Summary 2: Bt brinjal in India

> **Claim:** "Bt brinjal was developed by Mahyco in collaboration with Cornell University and approved for commercial cultivation in India in 2010 by GEAC. Following protests led by Greenpeace India and the coalition for GM-Free India, the Indian government imposed a moratorium in February 2010. The moratorium was lifted in 2024 following successful field trials in Bangladesh and the Philippines."

**Your task:** Verify each factual claim:
- [ ] Developer (Mahyco + Cornell)
- [ ] Year of GEAC approval (2010)
- [ ] Date of moratorium (February 2010)
- [ ] Whether moratorium was lifted in 2024
- [ ] Field trials in Bangladesh and Philippines

---

### Summary 3: MicroRNA in cancer

> **Claim:** "The discovery of microRNAs as oncogenes was made by Dr. Carlo Croce's lab at Ohio State University in 2002, published in Nature Genetics (DOI: 10.1038/ng848). The team showed that miR-155 is overexpressed in Burkitt lymphoma and acts as an oncogene by repressing the tumor suppressor gene MXI1."

**Your task:** Verify:
- [ ] DOI exists
- [ ] First author and lab
- [ ] Year (2002)
- [ ] miR-155 overexpression in Burkitt lymphoma
- [ ] MXI1 as target (vs other targets like TP53, BIM, etc.)

---

### Summary 4: COVID-19 mRNA vaccine

> **Claim:** "The Pfizer-BioNTech COVID-19 vaccine (BNT162b2) showed 95% efficacy in preventing symptomatic COVID-19 in the Phase 3 trial published in NEJM in December 2020 (Polack et al., DOI: 10.1056/NEJMoa2034577). The trial enrolled 43,548 participants and was conducted across 152 sites in 6 countries."

**Your task:** Verify:
- [ ] DOI exists
- [ ] First author (Polack)
- [ ] 95% efficacy claim
- [ ] Number of participants (43,548)
- [ ] Number of sites and countries

---

### Summary 5: Antibiotic resistance gene

> **Claim:** "The New Delhi metallo-beta-lactamase (NDM-1) gene was first identified in 2008 by Dr. Timothy Walsh's group in a patient who had received medical care in India. The gene confers resistance to all beta-lactam antibiotics including carbapenems and is now found in 80% of clinical isolates in Indian hospitals."

**Your task:** Verify:
- [ ] Year of discovery (2008)
- [ ] Researcher (Timothy Walsh)
- [ ] Original paper (likely Lancet Infectious Diseases)
- [ ] "80% of clinical isolates in Indian hospitals" — this sounds too high. Check.

---

## 🔍 Verification methods cheat sheet

### For DOIs
1. Copy the DOI
2. Go to https://doi.org/
3. Paste and search
4. If it resolves to a real paper → ✅
5. If "DOI not found" → 🚨 **fabricated DOI**

### For citations
1. Search Google Scholar with title + first author
2. Check the year, journal, volume, pages
3. Cross-reference with PubMed

### For gene names
1. Search the gene name in **UniProt** (https://www.uniprot.org/)
2. Check the official gene symbol (HGNC for human, MGI for mouse, etc.)
3. **Red flags:** Mixed case (Mir-155 vs miR-155), wrong organism prefix

### For statistics
1. Find the original paper (via DOI or PubMed)
2. Read the Results section
3. Check if the statistic exists
4. **Red flags:** Round numbers (60%, 80%), suspiciously clean

### For regulatory decisions (like Bt brinjal)
1. Check the official agency website (GEAC, ICMR, DCGI)
2. Look for press releases, gazette notifications
3. Cross-reference with reputable news (The Hindu, Indian Express, not just Wikipedia)

---

## 📊 Hallucination types — quick reference

| Hallucination type | How common | Time to verify | Red flags |
|--------------------|------------|----------------|-----------|
| **Fabricated DOI** | Very common (5-10% of AI citations) | 30 sec | DOI doesn't resolve |
| **Wrong authors** | Common | 1 min | Famous paper "by" obscure author |
| **Invented statistics** | Common | 2-5 min | Round numbers, too clean |
| **Wrong gene names** | Common in biology | 1 min | Non-standard naming |
| **Wrong pathway** | Very common | 5 min | Protein-to-pathway errors |
| **Outdated findings** | Common | 5-10 min | Pre-2020 data treated as current |
| **False "first" claims** | Very common | 5-10 min | "First X was done in year Y" |

---

## 🎓 Sample hallucination catch log

For Summary 4 (COVID-19 vaccine), here's an example:

> **Claim:** "BNT162b2 showed 95% efficacy in Phase 3 trial"
>
> **Verification method:** Searched PubMed for Polack et al. 2020 NEJM. Found the paper. Read Results section.
>
> **Actual finding:** 95% efficacy is correct for preventing symptomatic COVID-19.
>
> **However**, the **"152 sites in 6 countries"** claim is wrong. The actual trial was **152 sites in 6 countries** — wait, let me check. Actually that IS correct. Hmm.
>
> Let me check the participant count: The paper says **43,548 participants** — verified correct.
>
> **Verdict:** Summary 4 is actually accurate. No hallucination.
>
> **Time taken:** 4 minutes.

---

## ✅ Success criteria

You pass this lab if:
- [ ] You correctly identified hallucinations in at least 3 of the 5 summaries
- [ ] For each "no hallucination" verdict, you documented what you verified
- [ ] You used multiple verification methods (DOI lookup, PubMed search, UniProt, etc.)
- [ ] Your verification took less than 15 minutes per summary (aim for 5-10 min)

---

## 🚨 Common mistakes to avoid

### Mistake 1: Trusting AI by default
"AI said it, so it must be right." **No.** LLMs hallucinate 5-20% of the time on factual claims.

### Mistake 2: Skipping verification because "it sounds right"
Plausibility ≠ accuracy. DOIs that look valid often don't resolve.

### Mistake 3: Only checking the DOI
A real paper can have a real DOI but wrong year/wrong findings attributed to it.

### Mistake 4: Using only one verification method
If you only check the DOI and it resolves, you might miss a wrong author or wrong statistic.

**Fix:** Check DOI + PubMed + at least one cross-reference.

### Mistake 5: Not documenting your checks
If you can't show your verification, you didn't really verify.

---

## 🎯 Extension exercises (optional)

### Extension 1: Verify a paper you cited in your own work
Pick a recent paper you cited. Check every factual claim AI makes about it. How many hallucinations do you find?

### Extension 2: Compare Claude vs ChatGPT
Ask both the same biology question. Compare their hallucination rates. Document which is better for biology content.

### Extension 3: Test your university
Ask AI: "What research is being done at [your university] on [your topic]?" Verify the claims. Are alumni/faculty correctly listed?

### Extension 4: India-specific stress test
Ask AI: "What are the top 5 biology research institutions in India?" Check if any are fabricated.

---

## 📚 What's next

→ **[Lab 1.4: Build a literature matrix for your research question](./lab-1.4-literature-matrix.md)**

In the final Module 1 lab, you'll combine everything into a structured 10-20 paper literature matrix + 1-page field overview.

---

## 📖 Further reading

- **Paper:** "How Much Knowledge Can You Pack into the Parameters of a Language Model?" (Roberts et al., 2020) — shows LLMs memorize but also hallucinate
- **Tool:** [Scite.ai](https://scite.ai/) — shows whether a paper has been supported or contradicted by subsequent research
- **Tool:** [Retraction Watch](https://retractionwatch.com/) — database of retracted papers (always check if citing a controversial paper)

---

**🎓 Key takeaway:** Verification is not optional. It's the most important skill this course teaches.