# Module 2 — AI for Experimental Design

**Duration:** Week 2 (~8-10 hours)
**Outcome:** Use AI to generate hypotheses, design experiments with proper controls, calculate sample size, and verify protocols.

---

## Why this module matters

Bad experimental design = wasted 6-12 months + failed thesis chapter. AI can help you spot gaps **before** you start.

By end of this module, you'll have:
- 5 testable hypotheses for your research question
- A draft protocol with AI critique applied
- Sample size calculation with statistical justification
- A verified reagent list (no made-up catalog numbers)

---

## 📖 Lessons

### Lesson 2.1 — Hypothesis Generation (45 min)
**The problem:** Vague hypotheses lead to unfalsifiable experiments.

**You'll learn:**
- How to ask AI for testable hypotheses (not vague ones)
- The "falsifiability test" — would your hypothesis predict something different from null?
- 5 hypothesis templates: comparative, dose-response, mechanism, screening, validation
- **India case study:** Generating hypotheses from DBT mission document priorities

→ **[Lesson 2.1 notes](./01-hypothesis-generation.md)**

### Lesson 2.2 — Controls and Variables (60 min)
**The problem:** Missing controls = uninterpretable results.

**You'll learn:**
- Identifying missing controls in your protocol
- Positive vs negative controls vs standards
- Confounding variables in biology experiments
- **India context:** IAEC (Institutional Animal Ethics Committee) protocol requirements; CPCSEA guidelines

→ **[Lesson 2.2 notes](./02-controls-and-variables.md)**

### Lesson 2.3 — Sample Size and Power (75 min)
**The problem:** Underpowered studies = wasted research; overpowered = unethical animal use.

**You'll learn:**
- Statistical power basics (α = 0.05, power = 0.80)
- Using AI to draft statistical methods sections
- Common pitfalls: pseudoreplication, technical vs biological replicates
- **India context:** IAEC requirements for animal numbers (3Rs principle)

→ **[Lesson 2.3 notes](./03-sample-size-power.md)**

### Lesson 2.4 — Reagent and Protocol Lookup (45 min)
**The problem:** AI fabricates catalog numbers, buffer compositions, and reagent names.

**You'll learn:**
- AI vs protocol databases (Bio-protocol, protocols.io, Current Protocols)
- When AI is wrong about specific concentrations, pH, temperatures
- Cross-referencing with manufacturer datasheets
- **India context:** Sourcing reagents in India (Himedia, Sigma-Aldrich India, local suppliers)

→ **[Lesson 2.4 notes](./04-reagent-protocol-lookup.md)**

---

## 🧪 Labs

| Lab | Topic | Time | Difficulty |
|-----|-------|-----:|------------|
| **Lab 2.1** | Generate 5 hypotheses + falsifiability test | 90 min | 🟡 |
| **Lab 2.2** | Critique a real protocol (find 3 gaps) | 75 min | 🟡 |
| **Lab 2.3** | Sample size calculation for your experiment | 60 min | 🔴 |
| **Lab 2.4** | Verify AI protocol suggestions (3 examples) | 75 min | 🟡 |

---

## 🎯 Module 2 deliverables

- [ ] Lab 2.1: 5 hypotheses with falsifiability scores
- [ ] Lab 2.2: Protocol critique document (3+ gaps identified)
- [ ] Lab 2.3: Sample size calculation with justification
- [ ] Lab 2.4: Verification log for 3 AI protocol suggestions

---

## 🇮🇳 India-specific content

### IAEC protocol template (real)
Indian Institutional Animal Ethics Committees require:
1. Specific aim (1 paragraph)
2. Background (1 page max)
3. Justification for animal use (why no alternative?)
4. Animal details: species, strain, age, sex, weight, source
5. Number of animals + justification (3Rs: Replacement, Reduction, Refinement)
6. Experimental design (groups, treatments, endpoints)
7. Procedures (anesthesia, analgesia, euthanasia method)
8. Statistical analysis
9. Ethical considerations

**AI can draft this template. You must verify every claim against CPCSEA guidelines.**

### DBT funding priorities (2025-26)
Use these to align your hypotheses:
- Antimicrobial resistance
- One Health (human-animal-environment)
- Biotherapeutics and biosimilars
- Precision medicine
- Agricultural biotechnology (climate-resilient crops)
- Neurodegenerative diseases
- Maternal and child health

→ https://www.dbtindia.gov.in/

### Common Indian reagent suppliers
- **Himedia** (Mumbai) — broad catalog, good for media/buffers
- **Sigma-Aldrich India** — premium reagents
- **SRL (Sisco Research Laboratories)** — affordable alternative
- **Genei (Bangalore)** — molecular biology reagents
- **Merck India** — antibodies, kits
- **Local suppliers** (varied quality — verify lot numbers)

⚠️ AI tools often quote US/EU catalog numbers. Verify Indian availability and pricing before ordering.

---

## 🔧 Tools used

- **Claude / ChatGPT** — hypothesis generation, protocol critique
- **G*Power** (free) — sample size calculation
- **Bio-protocol** (free) — verified protocols
- **protocols.io** (free tier) — protocol database
- **GraphPad Prism** (paid, ₹30K/year) — advanced stats; or R/Python (free)

---

## ⚠️ Common mistakes

1. **Trusting AI's "typical" protocols** — "Standard PCR uses 35 cycles" is wrong for your specific gene; check primer Tm
2. **Ignoring Indian lab realities** — AI assumes -80°C freezers, ultrapure water, CO₂ incubators; not all Indian labs have all this
3. **Not checking reagent availability** — AI may suggest discontinued catalog numbers or US-only products
4. **Sample size too small** — "Use n=3" is rarely enough; do power analysis
5. **Sample size too large** — unethical for animal studies; IAEC will reject

---

## 📊 Self-assessment

Before moving to Module 3:
- [ ] I can generate 5 hypotheses in 15 minutes
- [ ] I can identify at least 3 missing controls in a protocol
- [ ] I can calculate sample size for t-test and ANOVA
- [ ] I can verify a reagent catalog number in 60 seconds

---

**Next:** [Module 3: AI for Data Analysis →](../03-data-analysis/README.md)