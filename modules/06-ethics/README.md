# Module 6 — AI Ethics & Responsible Use

**Duration:** Week 6 (~8-10 hours)
**Outcome:** Use AI as a biologist with full awareness of ethics, regulations, and limitations.

---

## Why this module matters

Most courses skip this. **It's the most important module.**

Using AI without understanding:
- Academic integrity rules → misconduct charge
- Data privacy laws → legal liability
- AI bias → bad science
- AI hallucinations → embarrassing errors

By end of this module, you'll have a personal AI usage policy + verification habits built into your workflow.

---

## 📖 Lessons

### Lesson 6.1 — What AI Should NOT Do (60 min)
- Diagnosis (clinical decisions) — never
- Final data interpretation without human review — never
- Anything requiring wet-lab verification you skip — never
- Replacing peer review — never
- Generating entire manuscripts from scratch — academic misconduct

### Lesson 6.2 — Academic Integrity (90 min)
- **UGC AI policy (2024)**
- **CSIR publication norms**
- **ICMR AI ethics draft (2025)**
- **Nature/Science/Cell AI use policies**
- What's allowed vs what's misconduct
- Disclosure requirements

### Lesson 6.3 — Data Privacy (60 min)
- **DPDP Act 2023** (India's data protection law)
- Don't paste patient data into public AI
- When to use local/private models (Llama, Mistral)
- Institutional policies

### Lesson 6.4 — Bias in Biological AI (75 min)
- Training data skew (Western-centric, model organism bias)
- How this affects literature review quality
- Underrepresentation of Indian research
- **Lab 6.4:** Identify 3 biases in AI-generated content

### Lesson 6.5 — When AI Is Wrong (90 min) ⚠️
- **Real case studies:**
  - Fabricated gene names
  - Wrong pathway assignments
  - Misattributed discoveries
  - Citation fabrication patterns
- How to build verification habits

---

## 🧪 Labs

| Lab | Topic | Time | Difficulty |
|-----|-------|-----:|------------|
| **Lab 6.1** | Audit your own AI usage (last 30 days) | 90 min | 🟡 |
| **Lab 6.2** | Write AI disclosure for your next paper | 60 min | 🟢 |
| **Lab 6.3** | Build a personal verification checklist | 75 min | 🟡 |
| **Lab 6.4** | Identify 3 biases in AI content | 60 min | 🔴 |

---

## 🎯 Module 6 deliverables

- [ ] Lab 6.1: Personal AI usage audit
- [ ] Lab 6.2: AI disclosure draft for next manuscript
- [ ] Lab 6.3: Personal verification checklist (10+ items)
- [ ] Lab 6.4: Bias identification report

---

## 🇮🇳 Indian regulations deep dive

### UGC AI policy (2024 circular highlights)

**Allowed:**
- AI for language editing and grammar
- AI for literature search assistance
- AI for data visualization suggestions
- AI for formatting references

**Not allowed:**
- AI as co-author or acknowledged contributor in research
- AI generating original hypotheses or interpretations without human authorship
- AI replacing critical thinking or analysis

**Required:**
- Disclosure in Methods or Acknowledgments
- Verification of all AI-generated content
- Maintaining human responsibility for all conclusions

### ICMR AI ethics draft (2025)

For clinical/medical biology:
- AI cannot make diagnostic or treatment decisions
- Patient consent required for AI-assisted care
- Algorithmic transparency mandatory
- Bias audits required for clinical AI tools
- Indian-specific validation required

### DPDP Act 2023 (Digital Personal Data Protection)

For biology research:
- Patient data must be anonymized before AI use
- Consent must cover AI processing
- Data localization requirements (for sensitive data)
- Penalties up to ₹250 Cr for violations

### Institutional policies (typical Indian university)
Most Indian universities (2024-25) require:
- IRB/IAEC approval for AI use in human/animal studies
- Data management plans for AI-processed data
- AI tool inventory (which tools you use, for what)
- Periodic audits

---

## 🚨 Real case studies — When AI went wrong in biology

### Case 1: Fabricated gene citation (Nature, 2023)
A submitted manuscript referenced a 2021 paper on KRAS gene variants. The DOI was fabricated by an AI tool. **Caught at revision stage.**

**Lesson:** Always verify DOIs before citing.

### Case 2: Wrong pathway assignment (bioRxiv preprint, 2024)
AI assigned a plant protein to a human disease pathway. The protein had no homolog in humans. **Caught by reviewers.**

**Lesson:** AI doesn't understand orthology well. Always verify pathway assignments.

### Case 3: Statistical fabrication (PLOS ONE, 2024 retraction)
Paper retracted because AI-generated statistics didn't match the raw data. **Caught by post-pub peer review.**

**Lesson:** Always re-run statistics yourself; don't trust AI's reported numbers.

### Case 4: Indian context ignored (PhD thesis, 2024)
Student used AI to write introduction, missed 8 highly-relevant Indian studies. Reviewer (Indian) caught it. **Thesis rejected, resubmitted.**

**Lesson:** AI is Western-centric. Always search Indian databases manually (Shodhganga, DBT).

### Case 5: Patient data leak (Case study, 2024)
Researcher pasted patient sequences into ChatGPT for "analysis." Sequences ended up in training data. **HIPAA/DPDP violation.**

**Lesson:** Never paste identifiable patient data into public AI. Use local models or anonymize.

---

## ⚠️ What AI should NEVER do in biology

1. **Make a clinical diagnosis** (e.g., "This patient has X")
2. **Recommend treatment** (e.g., "Patient should take drug Y")
3. **Sign off on laboratory results** (e.g., "These samples are COVID-positive")
4. **Replace peer review** (e.g., "This paper is acceptable")
5. **Make safety decisions** (e.g., "This GMO is safe for release")
6. **Be listed as an author** (per ICMJE, UGC, CSIR rules)
7. **Process identifiable patient data without consent** (per DPDP Act)
8. **Replace wet-lab verification** (e.g., "This primer will work, trust me")

---

## ✅ Verification habits to build

The "5-minute verification rule":

Before citing any AI-generated claim, spend **5 minutes** verifying:

1. ✅ DOI resolves
2. ✅ Authors + year + journal are correct
3. ✅ The paper actually says what AI claims
4. ✅ Statistics match the original paper
5. ✅ The paper is not retracted

**If any check fails, don't cite. Period.**

---

## 🔧 Tools for ethical AI use

| Tool | Use | Privacy |
|------|-----|---------|
| **Claude (Anthropic)** | Default — don't paste patient data | Opt-out available |
| **ChatGPT (OpenAI)** | Default — disable "Improve model for everyone" | Settings → Data controls |
| **Local Llama 3** | For sensitive data | Fully local |
| **Local Mistral** | Alternative local | Fully local |
| **Private GPT** | Enterprise option | On-prem |

For Indian biology research with sensitive data, consider **local models** on institute servers.

---

## 📜 Your personal AI usage policy (template)

```markdown
# My AI Usage Policy

## Tools I use:
- Claude (Anthropic) — primary writing assistant
- ChatGPT (OpenAI) — data analysis help
- Perplexity — literature search
- NotebookLM — paper synthesis

## What I use AI for:
✅ Grammar and language editing
✅ Outline generation
✅ Reference formatting
✅ Literature search suggestions
✅ Data visualization ideas

## What I NEVER use AI for:
❌ Diagnosis or clinical decisions
❌ Generating original research content without disclosure
❌ Processing patient data without anonymization
❌ Replacing peer review
❌ Skipping wet-lab verification

## Verification habits:
- Every DOI checked via https://doi.org/
- Every citation verified in PubMed
- Every statistic re-computed manually
- Every gene name verified in UniProt
- Every pathway assignment verified in KEGG/Reactome

## Disclosure:
I disclose AI use in Methods section of every manuscript.
```

→ **[Full template in `Lab 6.3`](./labs/lab-6.3-verification-checklist.md)**

---

## 📊 Self-assessment

Before starting capstone:
- [ ] I can articulate what AI should and should not do
- [ ] I know the UGC, CSIR, ICMR, DPDP rules for AI use
- [ ] I have a personal AI usage policy
- [ ] I have a 10-item verification checklist
- [ ] I can identify biases in AI-generated content

---

**Next:** [Final Capstone →](../../capstone/README.md)