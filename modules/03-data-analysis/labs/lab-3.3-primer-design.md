# Lab 3.3 — Design + Verify 3 Primer Pairs with AI

**Time:** 90 minutes
**Difficulty:** 🔴 Hard (most important bioinformatics lab)
**Tools:** Claude/ChatGPT, NCBI, UniProt, Ensembl, Primer-BLAST, dbSNP

---

## 🎯 Objective

Design 3 qPCR primer pairs for 3 different human genes using AI + NCBI verification. Document every verification step.

---

## 📋 What you'll submit

1. **AI prompts used** — copy-paste of your AI conversations
2. **Verification log** — for each gene, every database checked, every claim verified
3. **Primer pair report** — final primers + validation data (Tm, specificity, SNPs)
4. **Reflection** — when AI hallucinated, when it was right, when you overrode

---

## 🧬 The 3 genes

Choose from these (or pick your own):

| Gene | Function | Why interesting |
|------|----------|-----------------|
| **TP53** | Tumor suppressor | Most studied gene in cancer |
| **BRCA1** | DNA repair | Breast cancer risk |
| **MYC** | Transcription factor | Oncogene, regulates 15% of all genes |
| **GAPDH** | Housekeeping | Used as control |
| **BAX** | Pro-apoptotic | Part of apoptosis pathway |
| **BCL2** | Anti-apoptotic | BAX antagonist |
| **VEGFA** | Angiogenesis | Cancer, diabetic retinopathy |
| **HIF1A** | Hypoxia response | Cancer, altitude adaptation |

**For this lab, use these 3:**
1. **TP53** (tumor suppressor)
2. **BAX** (pro-apoptotic)
3. **GAPDH** (housekeeping control)

---

## 📝 Step-by-step instructions

### Step 1: Get accession numbers from AI (10 min)

**Use this prompt:**

```
I need to design qPCR primers for the following human genes:
1. TP53
2. BAX
3. GAPDH

For each gene, please provide:
- Current HGNC-approved official gene symbol
- NCBI RefSeq mRNA accession number (NM_*)
- Common aliases (with note that aliases should NOT be used in publications)
- Approximate mRNA length
- Number of transcript variants (canonical + others)
- Recommended primer design region (CDS, 5'UTR, 3'UTR?)

I will verify each item against HGNC (https://www.genenames.org/) and NCBI Gene 
(https://www.ncbi.nlm.nih.gov/gene/) before use.
```

**AI will likely return:**

| Gene | AI says | Will verify |
|------|---------|-------------|
| TP53 | NM_000546.6 | Check at NCBI |
| BAX | NM_004324.5 or NM_138761.4 (multiple variants) | Check which is canonical |
| GAPDH | NM_001289745.3 or NM_002046.7 (multiple) | Check which is standard |

### Step 2: Verify accession numbers (15 min)

For each gene, go to NCBI Gene and verify:

**Example for TP53:**
1. Go to https://www.ncbi.nlm.nih.gov/gene/7157
2. Check RefSeq: **NM_000546.6** (should be the transcript variant 1)
3. Check it says "tumor protein p53"
4. Check length: should be ~2.5 kb
5. Check status: should be "Reviewed" or "Validated" not "Predicted"

**Verification log template:**

```markdown
## TP53 verification

### AI claimed:
- Symbol: TP53
- Accession: NM_000546.6
- Length: ~2.5 kb

### Verified at NCBI Gene (https://www.ncbi.nlm.nih.gov/gene/7157):
- [ ] Official symbol matches HGNC: ✅
- [ ] Accession resolves to claimed gene: ✅
- [ ] Length matches: ✅ (2519 bp)
- [ ] Status: Reviewed ✅

### Decision: Use NM_000546.6 as the reference
```

### Step 3: Find CDS location + exon structure (10 min)

For each gene, go to NCBI Nucleotide and find the CDS:

**Example for TP53:**
1. Search for NM_000546.6 in NCBI Nucleotide
2. Open the GenBank flat file
3. Find the CDS line: `/note="NM_000546.6"`
4. Note CDS coordinates (e.g., 200-1500)
5. Find exons (look for `/exon` lines or use Ensembl)

**Easier alternative:** Use Ensembl's transcript page:
- https://www.ensembl.org/Homo_sapiens/Transcript/Summary?t=ENST00000269305
- Shows exon structure, CDS, UTRs

**Verification log:**

```markdown
## TP53 CDS location

### Source: NCBI GenBank NM_000546.6
- CDS: 203..1339 (1137 bp)
- 5'UTR: 1..202
- 3'UTR: 1340..2519

### Source: Ensembl ENST00000269305.9
- CDS: 11 exons, total 1182 bp
- Exon count matches NCBI: ✅

### Decision: Design primers in constitutive exons (present in all variants)
- Skip exons 2, 4, 9 (alternatively spliced in some variants)
- Use exons 5-6 boundary (good for qPCR)
```

### Step 4: Use NCBI Primer-BLAST (NOT AI for actual primer design) (20 min)

**For each gene:**

1. Go to https://www.ncbi.nlm.nih.gov/tools/primer-blast/
2. Settings:
   - PCR Template: paste your NM_ accession
   - Forward primer: leave blank
   - Reverse primer: leave blank
   - **Product size: 80-150 bp** (good for qPCR)
   - **Primer Tm: 59.0-61.0°C** (Max Tm difference: 1°C)
   - **Organism: Homo sapiens** (taxid 9606)
   - Database: **Refseq mRNA** (NM_)
   - **Specificity check: ✅ ON**
   - **Exon junction span: ✅ Prefer primers spanning exon-exon junctions**

3. Click "Get Primers"

4. **Primer-BLAST returns 5-10 primer pairs.** Pick the top one that:
   - Has Tm in your range
   - Spans an exon-exon junction (avoids amplifying genomic DNA)
   - Has high specificity (no off-target amplification)
   - Product size in your range

**For TP53 example:**

```
Primer pair 1:
- Forward: 5'-CCTCAGCATCTTATCCGAGTGG-3'
- Reverse: 5'-TGGATGGTGGTACAGTCAGAGC-3'
- Product size: 124 bp
- Tm: 60.2°C / 60.5°C
- Spans exon 5/6 junction: ✅
- Specificity: amplifies only TP53 (no off-targets)
```

### Step 5: Verify specificity (15 min)

**Primer-BLAST already does this** when you turn on specificity check. But double-check:

1. Go back to the Primer-BLAST results
2. Look for "Other targets on intended template" or "Non-specific products"
3. Confirm: only TP53 amplified (no TP63, TP73, etc.)
4. If off-targets detected: pick a different primer pair

**Also check with UCSC In-Silico PCR:**
1. Go to https://genome.ucsc.edu/cgi-bin/hgPcr
2. Paste your forward + reverse primers
3. Select genome: Human (GRCh38/hg38)
4. Click submit
5. Verify: amplifies TP53 region only, no other genomic regions

### Step 6: Check for SNPs in primer binding regions (10 min)

1. Go to https://www.ncbi.nlm.nih.gov/snp/
2. Search for your gene (e.g., "TP53")
3. Filter: "Clinical significance" = any, "Validation" = validated
4. Look for SNPs that fall in your primer binding regions
5. **India-specific:** Check allele frequencies in South Asian populations

**For TP53:**
- rs1042522 (P72R, codon 72 polymorphism) — VERY common (~30% in some populations)
- If your primer binds near this SNP, ~30% of samples may not amplify

**If SNP found in binding region:**
- Pick a different primer pair
- OR include the SNP as degenerate base (slightly less efficient but works)
- OR document that ~X% of samples may fail

### Step 7: Validate Tm with IDT OligoAnalyzer (5 min)

1. Go to https://www.idtdna.com/calc/analyzer
2. Paste your forward primer sequence
3. Set: [Salt = 50 mM Na+, 0 mM Mg2+] or [Salt = 50 mM Na+, 1.5 mM Mg2+]
4. Note Tm
5. Check for:
   - **Hairpin:** Should be ΔG > -3 kcal/mol (weak)
   - **Self-dimer:** Should be ΔG > -5 kcal/mol
   - **Hetero-dimer** (with reverse primer): Should be ΔG > -5 kcal/mol

**Repeat for reverse primer.**

### Step 8: Final primer pair report (10 min)

For each gene, document:

```markdown
## TP53 Primer Pair Report

### Reference:
- Gene: TP53 (tumor protein p53)
- HGNC symbol: TP53
- RefSeq: NM_000546.6 (verified at NCBI Gene)
- Verified at: https://www.ncbi.nlm.nih.gov/gene/7157

### Primer sequences:
- Forward: 5'-CCTCAGCATCTTATCCGAGTGG-3' (Tm = 60.2°C)
- Reverse: 5'-TGGATGGTGGTACAGTCAGAGC-3' (Tm = 60.5°C)
- Product size: 124 bp
- Spans exon 5/6 junction (avoids genomic DNA amplification)

### Specificity:
- Primer-BLAST: amplifies only TP53 (1 product)
- UCSC In-Silico PCR: confirms single product on chr17
- No off-targets detected

### SNP check:
- Checked dbSNP for common SNPs in binding regions
- rs1042522 (P72R) is downstream of binding site (no effect)
- No SNPs in primer binding regions at >1% global frequency

### Validation:
- Hairpin: ΔG = -1.2 kcal/mol ✅ (weak)
- Self-dimer: ΔG = -3.5 kcal/mol ✅ (weak)
- Hetero-dimer: ΔG = -4.1 kcal/mol ✅ (acceptable)

### Ready to order: YES
### Supplier recommendation: Sigma-Aldrich India (Himedia for budget option)
```

---

## ✅ Success criteria

You pass this lab if:
- [ ] All 3 primers designed using NCBI Primer-BLAST (not just AI)
- [ ] Each primer pair verified for:
  - Specificity (no off-targets)
  - Tm within range (verified by IDT)
  - No SNPs in binding regions (checked dbSNP)
  - No strong secondary structures (IDT OligoAnalyzer)
- [ ] Accession numbers verified at NCBI Gene
- [ ] AI hallucination log shows what AI got wrong (if anything)
- [ ] Each primer pair documented in a report

---

## 🚨 Common AI errors in primer design labs

### Error 1: AI gives primers instead of using Primer-BLAST
AI cannot calculate Tm accurately or check specificity. **Always use NCBI Primer-BLAST for actual primer sequences.**

### Error 2: AI suggests outdated gene symbols
- Old: c-myc → Current: MYC
- Old: p53 → Current: TP53
- Old: β-actin → Current: ACTB
- Verify each in HGNC

### Error 3: AI hallucinates accession numbers
Always verify NM_* accessions resolve to claimed gene.

### Error 4: AI doesn't consider transcript variants
BAX has NM_004324.5 (alpha) and NM_138761.4 (beta). Different proteins. Pick the canonical.

### Error 5: AI suggests primers that span intron >5kb
If your primers span a huge intron, PCR won't amplify from genomic DNA. But also won't work well for qPCR if intron is huge.

---

## 🇮🇳 India-specific primer considerations

### Population-specific SNPs
Check dbSNP for **South Asian allele frequencies**, not just global:

**Example TP53 SNPs more common in India:**
- rs1042522 (P72R): ~30% Arg/Arg in some Indian populations
- rs28934576: rare globally, slightly more common in some Indian groups

If your primer binding site overlaps with a common Indian SNP, ~30% of your Indian samples may not amplify.

### Reagent sourcing in India
- **Sigma-Aldrich India** — premium, fast delivery in metros
- **Himedia** (Mumbai) — affordable, Indian-made, good for standard primers
- **Eurofins India** — high quality, custom synthesis
- **Barcode Biosciences** (Bangalore) — affordable, growing
- **Imperial Life Sciences** — distributes multiple brands

**Cost:** ₹400-1500 per primer (depending on scale and purity). Always order HPLC-purified for qPCR.

### Shipping considerations
- Indian summer can damage primers in transit (heat > 40°C common)
- Order in winter if possible, or request cold shipping
- Store at -20°C immediately on arrival
- Avoid repeated freeze-thaw cycles (aliquot on arrival)

---

## 📤 What to submit

Submit a folder containing:
1. `ai_prompts.md` — copy-paste of AI conversations for each gene
2. `verification_log.md` — every database checked, every claim verified
3. `primer_pairs_report.md` — final primers + validation data
4. `hallucination_log.md` — what AI got wrong + how you caught it
5. Screenshots (optional but helpful): NCBI Gene pages, Primer-BLAST results, IDT OligoAnalyzer

---

## 🚀 Stretch goals

### Stretch 1: Order + test the primers
If you have lab access, order one primer pair and run qPCR. Did it work? Compare to predicted Tm/product size.

### Stretch 2: Design primers for a different organism
Try mouse (Trp53), Arabidopsis (AT5G...), or E. coli. Note organism-specific challenges.

### Stretch 3: Design primers for SNP genotyping
Design primers that specifically amplify one SNP allele (allele-specific PCR).

### Stretch 4: Compare AI tools
Try the same gene with Claude, ChatGPT, and Gemini. Compare their accession number suggestions. Which is most accurate?

---

## ❓ Troubleshooting

**Q: My primer has 2 products in Primer-BLAST. What do I do?**
A: Pick a different primer pair. Specificity is critical — 2 products = 2 different cDNAs amplified = your qPCR is useless.

**Q: The Tm is slightly off (e.g., 58.5°C). OK?**
A: Most qPCR machines work with 58-62°C. 58.5 is fine. Below 55°C is risky.

**Q: AI gave me a primer with a SNP. Should I exclude the SNP?**
A: Depends on SNP frequency. If <1% globally, ignore. If >5% in your population, redesign.

**Q: How do I know if my primer spans an exon junction?**
A: Check the primer position on the mRNA. If forward is in exon N and reverse is in exon N+1, it spans the junction. Primer-BLAST shows this.

**Q: My product size is 200 bp. Too big?**
A: For qPCR, 80-150 bp is ideal. Up to 300 bp is OK. >500 bp is too big (inefficient amplification).

---

## 📚 What's next

→ **[Lab 3.4: Compare AI vs human data interpretation](./lab-3.4-interpret-comparison.md)**

In the final Module 3 lab, you'll test your critical thinking against AI's interpretations.

---

**Time check:** If you took more than 90 min, that's expected for the first primer pair. Subsequent pairs should be faster (20-30 min each).