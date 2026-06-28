# Lesson 1.1 — Smart Paper Discovery

**Duration:** 45 minutes
**Video:** [Link to video]
**Outcome:** Find 10 relevant papers on any biology topic in 15 minutes.

---

## The problem

You open PubMed. You search for `CRISPR cancer therapy`. You get **8,432 results**. Now what?

Most biologists either:
- Read the first 20 results and miss key papers
- Spend hours filtering manually
- Give up and ask a colleague for "the important papers"

None of these are good. There's a better way.

---

## 🎯 The 5-tool discovery stack

Different tools are good for different jobs. Here's when to use each:

### 1️⃣ PubMed — the foundation
**Best for:** Comprehensive search, MeSH terms, official biomedical literature
**URL:** https://pubmed.ncbi.nlm.nih.gov/
**Free:** Yes

**When to use:**
- Starting a literature search
- Need comprehensive coverage of a biomedical topic
- Want to use controlled vocabulary (MeSH)
- Need citation export to EndNote/Zotero

**Limitations:**
- No AI summaries
- Limited to biomedical literature (no ecology, agriculture, etc.)
- Search can be overwhelming without proper filters

---

### 2️⃣ Semantic Scholar — AI-powered search
**Best for:** AI-ranked papers, citation context, "highly cited" discovery
**URL:** https://www.semanticscholar.org/
**Free:** Yes (no account needed)

**When to use:**
- Want to find "influential" papers, not just any paper
- Need to see citation context (why was this paper cited?)
- Want AI-generated TLDR summaries
- Looking across disciplines (not just biomedical)

**Special features:**
- **TLDR:** AI-generated 1-sentence summary
- **Highly Cited:** Filter to papers cited 100+ times
- **Citation Intent:** See if a citation is "background," "method," or "comparison"

---

### 3️⃣ Elicit — find papers by question
**Best for:** Finding papers that answer a specific research question
**URL:** https://elicit.com/
**Free:** 5,000 credits (enough for ~50 searches)

**When to use:**
- Have a specific research question, not just keywords
- Want to extract data from papers automatically
- Need to compare multiple papers' findings systematically

**Example query:** "What is the effect of CRISPR-Cas9 on lung cancer cell lines?"

Elicit returns papers + auto-extracts: sample size, methods, key findings, population.

---

### 4️⃣ Perplexity — web search with citations
**Best for:** Recent news, preprints, conference abstracts, regulatory updates
**URL:** https://www.perplexity.ai/
**Free:** Yes

**When to use:**
- Looking for very recent research (last 6 months)
- Need preprints (bioRxiv, medRxiv)
- Looking for clinical trial updates
- Want real-time citations (Perplexity shows where it got info)

**India-specific:**
- Great for finding DBT/ICMR announcements
- Finds regulatory documents (DCGI approvals)
- Good for searching Indian journals not in PubMed

---

### 5️⃣ NotebookLM — chat with your own papers
**Best for:** Synthesizing 5-10 papers you've already found
**URL:** https://notebooklm.google.com/
**Free:** Yes (with Google account)

**When to use:**
- After Lab 1.1, when you have 10+ PDFs
- Want to ask questions across multiple papers
- Need to find contradictions between papers
- Want audio summaries (Podcast feature)

**Workflow:**
1. Upload 10-20 PDFs to a notebook
2. Ask: "What methods did these papers use?"
3. Ask: "Where do these papers disagree?"
4. Get audio summary for commute listening

---

## 🔍 The 4-step discovery workflow

### Step 1: Define your question (5 min)

Bad: "CRISPR cancer"
Good: "Has CRISPR-Cas9 been used in clinical trials for solid tumors, and what were the outcomes?"

The good version:
- Has a specific population (solid tumors)
- Has a specific intervention (CRISPR-Cas9)
- Asks for outcomes
- Could be answered by multiple studies (PICO-style)

### Step 2: Run 3 parallel searches (5 min)

| Tool | Query |
|------|-------|
| **PubMed** | `"CRISPR-Cas9"[MeSH] AND "Solid Tumors"[MeSH] AND clinical trial[Publication Type]` |
| **Semantic Scholar** | `CRISPR Cas9 solid tumor clinical trial 2024 2025` (sort by citations) |
| **Perplexity** | `What are the latest CRISPR-Cas9 clinical trials for solid tumors in 2025?` |

Run all 3 in browser tabs. Don't optimize yet.

### Step 3: De-duplicate and filter (3 min)

Merge results into one spreadsheet. Remove duplicates. Apply filters:
- Last 5 years (unless landmark older paper)
- Human studies (if clinical) or animal/in vitro (if preclinical)
- English (unless you read other languages)
- Peer-reviewed (unless preprints are critical)

You should now have 20-30 papers.

### Step 4: Identify the "must-read" 10 (2 min)

Sort by:
1. **Citation count** (highly cited = influential)
2. **Recency** (newest = latest findings)
3. **Journal impact** (Nature/Science/Cell > specialty journals)
4. **Review papers first** (they synthesize the field)

Pick the top 10. These are your "must read" papers.

---

## 🇮🇳 India-specific tools and tips

### Free journal access for Indian universities

**INFLIBNET N-LIST:** https://nlist.inflibnet.ac.in/
- Free access to 6,000+ journals for Indian universities
- **How to register:** Ask your university librarian (they have admin access)
- Covers: Elsevier, Springer, Wiley, Taylor & Francis, etc.
- Alternative: **N-LIST for colleges** (separate scheme for non-university researchers)

### Indian thesis and research databases

| Database | URL | Content |
|----------|-----|---------|
| **Shodhganga** | https://shodhganga.inflibnet.ac.in/ | 300K+ Indian theses |
| **Indian Patents Database** | https://ipindiaservices.gov.in/ | Indian patents |
| **DBT e-Library** | https://www.dbtindia.gov.in/ | DBT-funded research |
| **CSIR Knowledge Gateway** | https://www.csir.res.in/ | CSIR lab publications |
| **ICMR Research** | https://www.icmr.gov.in/ | ICMR-funded research |

### Regional journal tips

Many high-quality Indian biology research is published in:
- **Indian Journal of Biochemistry and Biophysics** (NISCAIR)
- **Journal of Bioscience** (Indian Academy of Sciences)
- **Proceedings of the Indian National Science Academy**
- **Current Science** (IASc)
- **Indian Journal of Experimental Biology** (NISCAIR)

These are often missed by Western AI tools. **Always check Indian Science Abstracts** (NISCAIR publication) for completeness.

### Conference proceedings

AI tools miss these entirely:
- SBC (Society of Biological Chemists) — annual meetings
- Indian Biophysical Society
- Indian Immunology Society
- All India Cell Biology Conference

Contact the society directly for proceedings, or ask your supervisor.

---

## 🎓 Hands-on demo

In the video, I demonstrate finding every major paper on "CRISPR-Cas9 in solid tumor clinical trials" in 15 minutes.

**Result:** 12 highly relevant papers, including 3 reviews I would have missed using PubMed alone.

**Watch:** [Video timestamp 12:30]

---

## ⚠️ Common mistakes

### Mistake 1: Only using PubMed
You miss preprints, recent papers not yet indexed, conference abstracts, and non-biomedical angles.

### Mistake 2: Stopping at first 20 results
PubMed's default sort is "best match," which favors recent papers. Landmark older papers get buried.

**Fix:** Sort by "cited by" or "publication date" depending on your needs.

### Mistake 3: Not using MeSH terms
Free-text search misses synonymous terms. "Cancer" misses "neoplasm," "tumor," "malignancy," etc.

**Fix:** Always check the MeSH database for your topic. Use `[MeSH]` tags in PubMed.

### Mistake 4: Ignoring review papers
Reviews synthesize 50-200 papers. **Read the review first** — it tells you which primary papers matter.

### Mistake 5: Not saving your search
If you don't save the search, you'll redo it next month when you forget what you found.

**Fix:** PubMed → "Create alert" → get monthly emails with new papers matching your search.

---

## 🎯 Action items

Before moving to Lesson 1.2:

- [ ] Pick a research question (real or hypothetical)
- [ ] Run the 3 parallel searches (PubMed, Semantic Scholar, Perplexity)
- [ ] Build a list of 20-30 candidate papers
- [ ] Pick your top 10 "must-read" papers
- [ ] Save your PubMed search as an alert
- [ ] Set up a Google Sheet or Notion for your literature matrix (template in Lab 1.4)

---

## 📚 Additional resources

- **PubMed tutorials:** https://pubmed.ncbi.nlm.nih.gov/help/
- **MeSH browser:** https://meshb.nlm.nih.gov/
- **Boolean search cheat sheet:** (provided in supplementary materials)
- **Semantic Scholar API:** For power users, can automate searches

---

**Next lesson:** [Lesson 1.2 — Paper Summarization](./02-paper-summarization.md) →