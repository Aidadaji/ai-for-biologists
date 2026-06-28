# Lab 1.1 — Find 10 Papers on a Topic in 15 Minutes

**Time:** 60 minutes
**Difficulty:** 🟢 Easy
**Tools:** PubMed, Semantic Scholar, Perplexity, Google Sheets (or Notion)

---

## 🎯 Objective

Practice the 4-step discovery workflow by finding 10 highly relevant papers on a topic of your choice.

---

## 📋 What you'll submit

A Google Sheet (or Notion page) with:
- 10 papers (title, authors, year, journal, DOI, citation count)
- 1-paragraph "field overview" (200-300 words)
- 3 search queries you used (and why)

---

## 📝 Step-by-step instructions

### Step 1: Pick your topic (2 min)

Choose one of the following (or your own):

**Option A: Clinical**
- CRISPR-Cas9 in solid tumor clinical trials
- Monoclonal antibodies for autoimmune diseases
- mRNA vaccines beyond COVID-19 (cancer, HIV)

**Option B: Agricultural**
- Drought-resistant rice varieties (Indian context)
- Bt crops and pest resistance
- Biofortification of staple crops

**Option C: Ecology**
- Coral bleaching and microbiome
- Invasive species in Western Ghats
- Climate change impact on pollinators

**Option D: Neuroscience**
- Microglia in Alzheimer's disease
- Blood-brain barrier drug delivery
- Optogenetics in memory research

**Option E: Your own topic** (research project or thesis)

### Step 2: Run 3 parallel searches (5 min)

Open 3 browser tabs:

**Tab 1 — PubMed:**
```
[Your topic keywords] AND (review[Publication Type] OR clinical trial[Publication Type])
```
Apply filters:
- Last 5 years
- Humans (or your model organism)
- English

**Tab 2 — Semantic Scholar:**
- Search same keywords
- Sort by "Most Cited"
- Filter to last 5 years

**Tab 3 — Perplexity:**
- Ask: "What are the most important papers on [your topic] in the last 5 years?"
- Note the sources it cites

### Step 3: Merge and de-duplicate (3 min)

In your Google Sheet, create columns:
| # | Title | Authors | Year | Journal | DOI | Citations | Source |

Copy papers from all 3 tabs into one sheet. Sort by citation count (descending).

### Step 4: Pick your top 10 (2 min)

Selection criteria (in order of priority):
1. **Highly cited** (>50 citations is usually important)
2. **Recent** (2023-2025 papers for cutting-edge)
3. **Review papers** (they cover more ground)
4. **Top journal** (Nature/Science/Cell > specialty)
5. **Matches your PICO question** (Population, Intervention, Comparison, Outcome)

### Step 5: Write your field overview (3 min)

Synthesize what you learned. Use this template:

> **Field overview:** [Your topic] is an active area of research with [N] highly-cited papers in the last 5 years. The field focuses on [main themes]. Recent breakthroughs include [2-3 examples from your papers]. The remaining challenges are [2-3 open questions]. This literature matrix covers [N] papers spanning [date range].

---

## ✅ Success criteria

You pass this lab if:
- [ ] All 10 papers have DOIs
- [ ] All 10 papers are actually relevant (not just keyword-matched)
- [ ] Field overview is accurate (matches what papers actually say)
- [ ] You used all 3 tools
- [ ] Total time was under 20 minutes

---

## 🎓 Example submission

**Topic:** "CRISPR-Cas9 in solid tumor clinical trials"

**Top 10 papers found:** (DOI, citation count, year)
1. Nature 2024 — "CRISPR-Cas9 in solid tumors: A review" — DOI:10.1038/... — 234 citations
2. Science 2024 — "First-in-human CRISPR trial for ..." — DOI:10.1126/... — 189 citations
3. ... (8 more)

**Field overview (250 words):**
> CRISPR-Cas9 in solid tumor clinical trials is an emerging field with 234 highly-cited papers in the last 5 years. The field focuses on ex vivo edited T-cells (CAR-T with CRISPR knockouts) and in vivo lipid nanoparticle delivery. Recent breakthroughs include the first successful in vivo CRISPR editing in humans (2024, NEJM) and the FDA approval of Casgevy for sickle cell. The remaining challenges are delivery efficiency, off-target effects, and tumor heterogeneity. This literature matrix covers 10 papers spanning 2020-2025, with a focus on clinical (not preclinical) studies.

---

## 🚀 Stretch goals

If you finish early:

- **Stretch 1:** Find 5 more papers from Indian authors/research institutions (use Affiliation filter in PubMed)
- **Stretch 2:** Find 2 thesis chapters from Shodhganga on your topic
- **Stretch 3:** Find 1 patent related to your topic (Indian Patents Database)
- **Stretch 4:** Set up a PubMed alert for monthly updates

---

## ❓ Troubleshooting

**Q: I'm getting 10,000+ results. How do I narrow?**
A: Add more specific terms. Use quotation marks for exact phrases. Use MeSH terms. Apply publication type filters (clinical trial, review, meta-analysis).

**Q: My topic is very niche (e.g., a specific gene in a specific organism). Help?**
A: Search just for the gene name + organism. You might only find 5-10 papers total — that's fine for a niche topic.

**Q: All my papers are in one journal. Is that bad?**
A: Not necessarily — it means that journal is the leading venue for your topic. But try to find at least 2-3 papers from different journals to show breadth.

**Q: Can I use my thesis topic for this lab?**
A: Yes! That's actually the best use of this lab.

---

## 📚 What's next

→ **[Lab 1.2: Summarize 3 papers into a comparison table](./lab-1.2-summarize-papers.md)**

In the next lab, you'll take your top 3 papers from this lab and use AI to summarize them, then verify the AI's accuracy.