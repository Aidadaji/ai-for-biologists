# Lesson 3.3 — Bioinformatics Assistance with AI

**Duration:** 90 minutes
**Video:** [Link]
**Outcome:** Use AI for BLAST queries, primer design, and sequence interpretation — while catching the gene name hallucinations.

---

## The problem ⚠️

AI can help with bioinformatics, but it's also where AI hallucination is **most dangerous in biology**.

**Real failure modes:**
- Fabricated gene symbols (e.g., "MYC1" instead of "MYC")
- Wrong organism orthologs (suggesting a mouse gene is the same as a human one when it's not)
- Outdated gene names (using symbols deprecated 10 years ago)
- Hallucinated accession numbers (GenBank IDs that don't exist)
- Wrong primer Tm estimates (off by 5-10°C)
- Wrong protein function annotations (AI invents functions)

**This lesson trains you to use AI for speed but verify with authoritative databases.**

---

## 🎯 What you'll learn

1. The authoritative bioinformatics databases (NCBI, UniProt, Ensembl)
2. How to use AI as a "smart search bar" for these databases
3. Primer design with AI assistance + NCBI Primer-BLAST verification
4. Sequence interpretation (BLAST, alignment)
5. Protein function annotation (GO terms, pathways) with verification
6. India-specific: GIPMER, Indian Biological Data Centre

---

## 🗄️ The authoritative databases (your source of truth)

**Always verify AI outputs against these. No exceptions.**

### NCBI (National Center for Biotechnology Information)
**URL:** https://www.ncbi.nlm.nih.gov/
**Use for:** Gene sequences, BLAST, Primer-BLAST, PubMed, dbSNP, GenBank
**Free:** Yes
**Indian mirror:** Works fine from India; ERNET provides faster access

**Key tools:**
- **BLAST:** https://blast.ncbi.nlm.nih.gov/ — sequence similarity search
- **Primer-BLAST:** https://www.ncbi.nlm.nih.gov/tools/primer-blast/ — primer design + specificity check
- **Gene:** https://www.ncbi.nlm.nih.gov/gene/ — gene information
- **Nucleotide:** https://www.ncbi.nlm.nih.gov/nuccore/ — DNA sequences
- **Protein:** https://www.ncbi.nlm.nih.gov/protein/ — protein sequences

### UniProt
**URL:** https://www.uniprot.org/
**Use for:** Protein sequences, function, GO terms, isoforms
**Free:** Yes

**Key tools:**
- **UniProtKB** — manually curated protein knowledgebase
- **UniParc** — archive of all protein sequences
- **ID mapping** — convert between gene IDs (Ensembl ↔ Entrez ↔ HGNC ↔ UniProt)

### Ensembl
**URL:** https://www.ensembl.org/
**Use for:** Gene annotation, comparative genomics, variation
**Free:** Yes

### GeneCards
**URL:** https://www.genecards.org/
**Use for:** Human gene summary (one-stop shop)
**Free:** Yes

### HGNC (Human Gene Nomenclature Committee)
**URL:** https://www.genenames.org/
**Use for:** Authoritative human gene names + symbols
**Free:** Yes

### KEGG / Reactome
**URL:** https://www.genome.jp/kegg/ | https://reactome.org/
**Use for:** Pathway assignments
**Free:** Yes (KEGG now restricted for some uses; check license)

### India-specific
- **DBT (Department of Biotechnology)** — https://dbt.gov.in/ (covers BTISnet + Genome India Project)
- **Indian Biological Data Centre** — https://ibdc.dbtindia.gov.in/ (still active)

---

## 🧬 Primer design workflow (with AI + verification)

### The wrong way (full AI)

```
You: "Design primers for human TP53"
AI: "Forward primer: 5'-ATGGAGGAGCCGCAGTCAG-3'
     Reverse primer: 5'-GTCGTCGTCGTCGTCTCTG-3'"
```

**DON'T TRUST THIS.** The primers may not work, may amplify wrong products, may not be specific.

### The right way (AI + NCBI verification)

**Step 1: Get the right accession number (use AI, verify in NCBI)**

```
You: "What's the NCBI RefSeq mRNA accession for human TP53?"
AI: "NM_000546.6"
```

**Verify:** Go to https://www.ncbi.nlm.nih.gov/nuccore/NM_000546.6
- ✅ Should resolve to "tumor protein p53"
- ✅ Length: ~2.5 kb
- ✅ Updated: within last 5 years

**Step 2: Find the CDS (coding sequence)**

```
You: "What is the CDS (coding sequence) location in NM_000546.6?"
AI: "130-1431"
```

**Verify:** Look at the GenBank file. CDS should be marked.

**Step 3: Use NCBI Primer-BLAST (NOT AI for primer design)**

```
Go to: https://www.ncbi.nlm.nih.gov/tools/primer-blast/

Settings:
- PCR Template: NM_000546.6
- Forward primer: leave blank
- Reverse primer: leave blank
- PCR product size: 100-300 (for qPCR)
- Primer Tm: 59-61°C (default)
- Max Tm difference: 1°C
- Organism: Homo sapiens
- Database: Refseq mRNA
- Specificity check: ✅ ON
```

Primer-BLAST will return:
- Primer sequences
- Predicted Tm
- Self-complementarity scores
- **Most importantly:** what other genes these primers might amplify

**Step 4: Verify with in silico PCR**

Use UCSC In-Silico PCR: https://genome.ucsc.edu/cgi-bin/hgPcr

Paste your primers, see if they amplify the expected product + check for off-targets.

**Step 5: Check for SNPs in primer binding regions**

Use dbSNP: https://www.ncbi.nlm.nih.gov/snp/

If a primer binding site has a common SNP (especially in Indian populations), the primer may not work for some samples.

**India-specific:** Check Indian population allele frequencies in GIPMER or dbSNP's population genetics data.

---

## 🚨 Common AI errors in bioinformatics

### Error 1: Fabricated gene symbols

**Test:** Ask AI for "10 cancer driver genes" and check each in HGNC.

**Real example:**
- AI suggests: "PIK3CA, TP53, KRAS, MYC, EGFR, BRCA1, BRCA2, PTEN, APC, **CDKN2A**"
- AI suggests (bad version): "PIK3CA, TP53, KRAS, **MYC1**, EGFR, BRCA1, BRCA2, PTEN, APC, CDKN2A"
- "MYC1" is a real gene but VERY rare — AI should suggest "MYC" (the famous oncogene)

**How to catch:** Every gene goes through HGNC before you order primers.

### Error 2: Wrong organism

**Real example:** Asking AI for "mouse p53 primers" might return human primers (because p53 is famous in human context).

**How to catch:** Specify organism + verify accession number is from correct organism.

### Error 3: Outdated gene names

**Real example:**
- Old name: "P16"
- Current HGNC-approved: "CDKN2A"
- AI may still use "P16" because it's in older literature

**How to catch:** Check HGNC for current approved symbol.

### Error 4: Hallucinated accession numbers

**Test:** Ask AI for 5 random GenBank accessions and check each.

**Real example:** AI might give "NM_001234.5" which resolves to a completely different gene than what AI claimed.

**How to catch:** Every accession verified via direct URL (https://www.ncbi.nlm.nih.gov/nuccore/NM_XXXXX).

### Error 5: Wrong primer Tm

**Real example:** AI might quote Tm = 62°C for a primer that actually has Tm = 57°C. 5°C error = poor amplification.

**How to catch:** Use IDT OligoAnalyzer (https://www.idtdna.com/calc/analyzer) or NCBI Primer-BLAST, which calculate Tm accurately.

### Error 6: Missing splice variants

Genes often have multiple transcript variants. AI may design primers that only amplify one variant (usually the canonical, but not always).

**How to catch:** Use Ensembl to check all transcript variants. Design primers in constitutive exons (present in all variants) if you want to detect all.

### Error 7: Wrong pathway assignments

**Real example:** AI might assign a protein to a pathway it doesn't actually participate in.

**How to catch:** Verify in KEGG or Reactome. Search the protein, check which pathways list it.

---

## 📋 Pre-flight checklist for AI bioinformatics

Before trusting ANY AI-generated bioinformatics output:

| Step | Verify | Tool |
|------|--------|------|
| 1 | Gene symbol is current | HGNC |
| 2 | Accession resolves to claimed gene | NCBI Nucleotide |
| 3 | Sequence length matches | NCBI |
| 4 | CDS location correct | GenBank file annotation |
| 5 | Primer Tm within range | NCBI Primer-BLAST |
| 6 | Primers specific (no off-targets) | NCBI Primer-BLAST |
| 7 | No common SNPs in binding site | dbSNP |
| 8 | Works for target organism | Organism-specific database |
| 9 | Pathway assignment correct | KEGG / Reactome |
| 10 | Function annotation accurate | UniProt + GO terms |

**Time for verification:** 5-15 minutes per primer pair.
**Cost of skipping verification:** Wasted weeks + ₹10-50K in reagents.

---

## 🤖 Good AI prompts for bioinformatics

### Prompt 1: Get gene info (with verification plan)

```
I need information about the human [GENE] gene for designing a qPCR experiment.

Please provide:
1. Current HGNC-approved official gene symbol
2. NCBI RefSeq mRNA accession number
3. Common aliases (with note that aliases are NOT to be used in publications)
4. Genomic location (chromosome)
5. Number of transcript variants
6. Recommended primer design region (CDS, 5'UTR, 3'UTR?)
7. Housekeeping gene alternatives (if relevant)

I will verify each item against HGNC, NCBI Gene, and Ensembl before use.
```

### Prompt 2: Interpret a BLAST result

```
I ran BLAST with my protein sequence against human RefSeq proteins.

Top hit: [description, E-value, identity, coverage]
Second hit: [description, E-value, identity, coverage]

Please help me interpret:
1. Is this likely a homolog or just a related family member?
2. What functional clues does the hit provide?
3. Should I investigate the second hit too?

I'll verify the function annotations against UniProt and the literature.
```

### Prompt 3: Design qPCR primers (with NCBI verification)

```
I need to design qPCR primers for human [GENE].

Requirements:
- Product size: 80-150 bp
- Tm: 59-61°C
- Should span exon-exon junction (to avoid amplifying genomic DNA)
- Specificity: should amplify only [GENE], not paralogs

I'll use NCBI Primer-BLAST to design and verify the primers you suggest.
Please give me:
1. Approximate region of the mRNA to target
2. Exons that should be included/excluded
3. Known SNPs to avoid
4. Any paralogs I should exclude

Don't give me the actual primer sequences — I'll design those in Primer-BLAST.
```

---

## 🇮🇳 India-specific bioinformatics

### GIPMER (Genome India Project)
- **URL:** https://dbt.gov.in/scientific-programmes (now under DBT)
- **Use for:** Indian population-specific genetic variants
- **Why it matters:** Many variants are rare globally but common in Indian populations
- **Example:** CYP2C19 variants differ in frequency between Indian and European populations, affecting drug metabolism

### Indian Biological Data Centre (IBDC)
- **URL:** https://ibdc.dbtindia.gov.in/
- **Use for:** Indian genomics data (sequence read archive, etc.)
- **Why it matters:** Hosts Indian-specific sequence data not in international databases

### Bt brinjal bioinformatics case study (real)
The GM regulatory discussion in India involved bioinformatic analysis of:
- cry1Ac gene insertion site
- Potential allergenicity (BLAST against allergen databases)
- Comparative genomics with native eggplant proteins

**Lesson for AI users:** Many of these analyses were done manually by GEAC experts because AI tools (in 2010) couldn't reliably handle these complex multi-step analyses.

**Today:** AI can help draft the bioinformatics pipeline, but each step still needs verification against authoritative databases.

---

## 🧪 Lab preview

In Lab 3.3, you'll:
1. Design primers for 3 different genes using AI + NCBI Primer-BLAST
2. Verify each primer pair for specificity, Tm, SNPs
3. Document the entire verification workflow
4. Submit a "primer validation report" that could go in your thesis Methods section

---

## 🎯 Hands-on demo

In the video, I demonstrate:
1. AI suggesting primer design region → verified in NCBI
2. NCBI Primer-BLAST for actual primer sequences
3. Checking specificity (no off-targets)
4. Checking dbSNP for SNPs in binding regions
5. Generating a primer validation report

**Watch:** [Video timestamp 38:00]

---

## 🎯 Action items

Before moving to Lesson 3.4:

- [ ] Pick a gene you're working on (or hypothetical)
- [ ] Use AI to get accession number + gene info
- [ ] Verify in HGNC and NCBI
- [ ] Design primers in NCBI Primer-BLAST
- [ ] Check specificity (no off-targets)
- [ ] Document verification in a report

---

## 📚 Additional resources

- **AlterLab skills used:**
  - `alterlab-blast` — BLAST queries and interpretation
  - `alterlab-primer-design` — primer design + verification
  - `alterlab-uniprot` — protein verification
  - `alterlab-ncbi-tools` — NCBI resource navigation
- **Free databases:**
  - **NCBI** — ncbi.nlm.nih.gov
  - **UniProt** — uniprot.org
  - **Ensembl** — ensembl.org
  - **Primer3Plus** — alternative to Primer-BLAST
  - **UCSC Genome Browser** — genome.ucsc.edu
- **Indian resources:**
  - **GIPMER** — genomeindia.nii.ac.in
  - **IBDC** — ibdc.dbtindia.gov.in
  - **IISc Bioinformatics Facility** — courses for Indian researchers

---

## ⚠️ Common mistakes

### Mistake 1: Trusting AI for primer design
AI can suggest regions, but actual primer design needs NCBI Primer-BLAST (or similar) for specificity checks.

### Mistake 2: Not checking for paralogs
Many genes have paralogs (similar sequences from gene duplication). Primers may amplify the paralog too.

### Mistake 3: Ignoring SNPs
If your primer binding site has a SNP at >5% frequency, ~5-10% of samples won't amplify.

### Mistake 4: Using non-RefSeq accessions
Some accessions are predicted, not validated. Always prefer RefSeq (NM_*, NP_*) over GenBank (e.g., M_, X_).

### Mistake 5: Not considering transcript variants
A gene may have 5 transcript variants. Your primers may amplify only 1 or 3 of them.

### Mistake 6: Forgetting species for model organisms
If studying mice, mouse gene names are capitalized differently (e.g., Trp53 vs TP53).

---

**Next lesson:** [Lesson 3.4 — Interpreting AI Analysis](./04-interpreting-ai-analysis.md) →