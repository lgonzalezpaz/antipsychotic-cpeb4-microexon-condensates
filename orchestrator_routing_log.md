# Orchestrator Multi-Agent Routing & Verification Log

- **Project**: Antipsychotic Restoration of *CPEB4* Microexon 4 Splicing and Condensate Reversibility
- **Coordinator Model**: Orchestrator (Neon)
- **Routing Criterion**: Complexity × Risk decision matrix (Low/Low → Flash; Medium/Medium → Inherit/Standard; High/High → Pro; escalate automatically upon failure or inconsistency).

| Step | Subagent Role | Assigned Model Tier | Complexity | Risk | Scope & Verification Criterion | Status |
|---|---|---|---|---|---|---|
| 1 | `Bioinformatics-Data-Curator` | `inherit` (Standard) | Medium | Medium | Ingest 8 public databases (GTEx v8, GSE276143, RefSeq/UniProt, ChEMBL 37, STRING v12.5, GSE138082, GSE174407, GSE163161/GSE315204/GSE67755), compute SHA256 manifest (`164` files, `591.36 MB`), run partial/covariate-adjusted stats & meta-analysis. Zero NaNs verified. | COMPLETED |
| 2 | `Literature-Evidence-Verifier` | `inherit` (escalate to `pro` on conflicts) | Medium–High | High | Query PubMed E-utilities & CrossRef API for `55/55` primary citations (`100%` HTTP 200, `title_match_score=1.00`, claim-to-abstract audit passed), write `data/verified_references.json` & `verified_references_audit.csv`. | COMPLETED |
| 3 | `Math-Biophysics-Modeler` | `pro` (script authoring) → `inherit` (execution, iterative debugging & verification after `pro` 429 quota exhaustion) | High | High | Derive, verify analytically, calibrate (`GSE276143`, `GTEx v8`, `Garcia-Cabau 2025`, `ChEMBL 37`), cross-validate (LOOCV), run Sobol/PRCC GSA, Arm 1/2/3 ablations, and bifurcation/iPSC predictions for the 16-equation RC-KTF model. `ALL_TESTS_PASSED=True`, zero NaNs across all 10 tables. | COMPLETED |
| 4 | `Audit-Order-Formatter` | `flash` | Low–Medium | Medium | Visually verified all 9 PNG figures, independently ran `run_all.py --from-processed --skip-modeling` (`81.20 s`, exit `0`) and `07_audit_manuscript.py` (`46/46` PASS, `ALL_CHECKS_PASSED=true`, `16/16` native `<m:oMath>` equations in DOCX, strict `1..N` order across Equations/Tables/Figures/Supp/54 Refs, zero stray tokens or AI leaks). | COMPLETED |
