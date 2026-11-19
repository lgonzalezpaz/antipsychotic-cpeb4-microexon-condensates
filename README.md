# Antipsychotic Signaling Convergence on *CPEB4* Microexon 4 Splicing and Condensate Proteostasis

This repository provides the complete public data curation, bioinformatics, biophysical modeling, mathematical verification, figure generation, and automated manuscript-assembly pipeline accompanying the manuscript:

> **Antipsychotic signaling converges on SRRM4 phosphorylation, HDAC2-mediated RNA polymerase II slowing, and autophagic proteostasis to rescue CPEB4 microexon 4 condensates**

## Key Scientific Findings

1. **Master Splicing Factor Identity (*SRRM4* vs *RBFOX1*)**: Human *CPEB4* microexon 4 (`24 nt`, encoding `+4`-charged `ARTYGRRR`) exhibits a `−7.79 bit` 3' splice-site deficit relative to downstream exon 5, `53` upstream hnRNPC/PTBP1 poly-U tracts, an embedded `−5 nt` SRRM4 `TGC` motif, and zero RBFOX `(T)GCATG` motifs within `±300 nt`. Controlling for neuronal abundance (*RBFOX3* + *SYP*) across 13 GTEx v8 brain regions turns *RBFOX1* partial correlation negative (*r* = −0.621, *P* = 0.0415) while retaining strong positive associations for *SRRM3* (+0.882), *RNPS1* (+0.853), *SRSF11* (+0.732), *HDAC2* (+0.715), *SRPK1* (+0.714), and *SRRM4* (+0.701).
2. **Phosphorylation vs Chromatin–Pol II Kinetics**: Random-effects meta-analysis across 5 cross-species antipsychotic cohorts (*N* = 104) eliminates bulk *SRRM4* transcriptional induction (*g* = −0.696, FDR = 0.0202, *I*² = 9.6%) while identifying conserved *PTBP1* suppression (*g* = −0.676, *I*² = 0%) and human neuronal *HDAC2* induction (*g* = +0.794, *I*² = 0%, *N* = 78) with *POLR2A* decrease (*Z* = −3.056). Model ablation proves that PKA/DARPP-32/PP1–CaMKII phosphorylation (+4.58% ΔΨ₄), hyperexcitability relief (+6.64%), and 5-HT2AR–HDAC2–Pol II elongation deceleration (+7.08%) combine to deliver +10.36 percentage points of threshold epistasis (+39.0% over additive sum) in Day-28 condensate fluidity.
3. **Condensate Prevention vs Clearance Hysteresis**: Heterotypic `me4`–HClust buffering coupled to asymmetric turnover (*t*₁/₂,*L* = 2 d vs *t*₁/₂,*S* = 10 d) creates saddle-node bistability (Ψ₄* ∈ [0.66, 0.76]), separating passive autophagic clearance in moderate burden (*M*_f(42 d) = 0.657 under risperidone) from prion-like monotherapy lock-in (*M*_f(42 d) = 0.252), which is rescued by 2× autophagy (0.818) or `0.5 eq` synthetic `me4` peptide (0.732).

## Repository Structure

```text
antipsychotic-cpeb4-microexon-condensates/
├── data/
│   ├── raw/sha256_manifest.json        # SHA256 verification ledger for 164 cached raw files (591.36 MB)
│   ├── processed/                      # Standardized cohort tables, ChEMBL Ki, STRING graph, cis architecture
│   └── verified_references.json        # 55 PubMed/CrossRef-verified reference records
├── scripts/
│   ├── 01_fetch_public_databases.py    # Public API/FTP ingestion + SHA256 verification
│   ├── 02_bioinformatics_analysis.py   # Sequence PWM/motifs, GTEx partial r, GEO OLS, DL meta-analysis
│   ├── 03_mechanistic_model_and_validation.py # 16-eq RC-KTF model, analytical verification, CV, Sobol GSA
│   ├── 04_verify_literature.py         # Live PubMed E-utilities + CrossRef title & claim verification
│   ├── 05_generate_figures.py          # 600-DPI PNG + SVG/PDF publication figures (Fig. 1-6, S1-S3)
│   ├── 06_build_manuscript_docx.py     # Native editable OMML Word DOCX & Markdown manuscript builder
│   ├── 07_audit_manuscript.py          # Automated sequential order, OOXML, citation & watermark auditor
│   └── run_all.py                      # End-to-end master reproduction runner
├── results/
│   ├── metrics_registry.json           # Canonical numerical registry
│   ├── verification_report.json        # 11/11 analytical & solver checks passed
│   ├── manuscript_audit_report.json    # Complete manuscript, OOXML, & citation audit report
│   └── tables/                         # Table 1-4, Table S1-S4, and intermediate outputs (zero NaNs)
├── figures/                            # Figure1-6 & FigureS1-S3 in PNG (600 DPI), SVG, and PDF
├── manuscript/                         # Manuscript.md, Manuscript_with_Figures.docx, Manuscript_Text_Only.docx, Supplementary_Material.*
├── environment.yml
├── requirements.txt
├── DATA_INSTRUCTIONS.md
├── FILE_LIST_GitHub_Zenodo.txt
├── CITATION.cff
├── LICENSE
└── orchestrator_routing_log.md
```

## Quick Reproduction Instructions

```bash
conda env create -f environment.yml
conda activate cpeb4-antipsychotic

# Option 1: Rapid reproduction from processed tables (skips ~7 min Sobol/bootstrap modeling)
python scripts/run_all.py --from-processed --skip-modeling

# Option 2: Complete mathematical modeling + figures + manuscript + audit from processed data
python scripts/run_all.py --from-processed

# Option 3: Full live public database download + entire pipeline (~15-20 min)
python scripts/run_all.py
```

If raw files from an archive have already been downloaded to `data/raw/`, run `python scripts/run_all.py --skip-download` to verify all 164 SHA256 hashes before executing stages `02`–`07`.

## License & Citation

Released under the [MIT License](LICENSE). See [CITATION.cff](CITATION.cff) for software/data citation metadata.
