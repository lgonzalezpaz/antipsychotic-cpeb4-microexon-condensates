# Public Data Retrieval & Reproducibility Instructions

All empirical analyses in this repository use freely accessible public biological databases. No restricted-access controlled datasets are required.

## 1. Automated Retrieval (Default)

Run from the repository root:

```bash
python scripts/01_fetch_public_databases.py
```

This caches raw API responses and GEO files into `data/raw/` and verifies cryptographic SHA256 digests against `data/raw/sha256_manifest.json`:

1. **GTEx Portal v8 API** (`https://gtexportal.org/api/v2/`): `CPEB4` (`ENSG00000113742.12`) median junction/exon expression and 31 regulatory genes across all 54 tissues (13 brain subregions).
2. **NCBI GEO `GSE276143`** (`https://ftp.ncbi.nlm.nih.gov/geo/series/GSE276nnn/GSE276143/suppl/`): All 6 biological replicate exon-inclusion tables (`GSE276143_T0_INCLUSION_TABLE_rep1..6.tab.gz`) for human *CPEB4* microexon 4 (`HsaEX0016976`).
3. **NCBI RefSeq & UniProtKB**: Genomic span `NC_000005.10:173932440-173945150` via NCBI E-utilities (`efetch`) and curated protein entries `Q17RY0`, `A7MD48`, `Q9NWB1`, `P14416`, `P28223`, `Q9UD71`, `Q92769` via `https://rest.uniprot.org/uniprotkb/`.
4. **ChEMBL 37 REST API** (`https://www.ebi.ac.uk/chembl/api/data/`): Experimental human `Ki` (`nM`) binding records for 12 antipsychotics across 7 GPCR targets (`DRD2`, `HTR2A`, `DRD1`, `HTR1A`, `ADRA1A`, `HRH1`, `CHRM1`).
5. **STRING v12.5 REST API** (`https://string-db.org/api/json/network`): Curated human (`species=9606`) 27-node signaling-to-splicing interaction graph (`required_score=400`).
6. **NCBI GEO `GSE138082`** (`https://ftp.ncbi.nlm.nih.gov/geo/series/GSE138nnn/GSE138082/`): Human hippocampal subfield (CA1/CA3/DG) RNA-seq counts (`n = 78`) and series matrix metadata.
7. **NCBI GEO `GSE174407`** (`https://ftp.ncbi.nlm.nih.gov/geo/series/GSE174nnn/GSE174407/`): Human frontal cortex `NeuN+` neuronal RNA-seq `featureCounts` files (`116` technical files merged into `58` independent donors) + HGNC symbol mapping (`hgnc_complete_set.txt`).
8. **Cross-species Pharmacological GEO Datasets**:
   - `GSE163161`: Human iPSC-derived Ngn2 excitatory neurons exposed to clozapine (`n = 10`).
   - `GSE315204`: Sorted mouse frontal cortex `THY1+` neurons, `HEPA` astrocytes, and `CD45+` microglia treated with vehicle, risperidone, or clozapine (`n = 18`).
   - `GSE67755`: Chronic haloperidol vs placebo mouse brain expression matrix (`GPL11533` microarray, `n = 20` whole brains) + `GPL11533.annot.gz`.
9. **PubMed E-utilities & CrossRef API**: Verified metadata for all 55 primary references (`python scripts/04_verify_literature.py`).

## 2. Offline / Cached Mode (Release Archive)

Because the full raw download cache totals `591.36 MB` across `164` files (primarily the 116 individual `GSE174407` count files), the portable GitHub/Zenodo release archive bundles the compact donor-merged count matrix (`data/processed/gse174407_neun_donor_counts.csv.gz`, `2.79 MB`), all processed analytical CSV/JSON files (`data/processed/`), `data/raw/sha256_manifest.json`, and `data/verified_references.json`.

To regenerate every table, figure, verification report, and manuscript from the processed cache without downloading `591 MB` of raw GEO files:

```bash
python scripts/run_all.py --from-processed
```

To run the complete pipeline starting from raw downloads (or verifying existing `data/raw/` hashes):

```bash
python scripts/run_all.py
```
