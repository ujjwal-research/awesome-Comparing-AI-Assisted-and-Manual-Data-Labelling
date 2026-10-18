# Gate G1 - One-Page Research Brief

**Course:** AI Tools for Research - ATR PostMid  
**Student:** Ujjwal Nikam | **Enrollment:** [to confirm]  
**Study status:** Planned; no code runs or measured results yet.  
**Working title:** Budget-Constrained Uncertainty-Guided Verification of Scientific Citation-Intent Labels

## Review foundation and verified sources
Previous review: *Comparing AI-Assisted and Manual Data Labelling Accuracy on Scientific Datasets* (Section 6: integrating active learning with AI-assisted verification; standardised accuracy-effort reporting). Original sources checked: Cohan et al. (2019), Settles (2009), Gilardi et al. (2023), Northcutt et al. (2021). The proposed gap is a **specific course-level comparison**, not a verified claim of algorithmic novelty.

## Gap and research question
**Gap:** The previous review identifies inadequate system-level evidence about allocating limited verification effort. Scientific citation-intent labelling is a tractable setting to test label-review prioritisation under controlled budgets. Active learning ordinarily selects training examples; here we test *post-prediction oracle correction*, not conventional active learning.

**Primary RQ:** On SciCite, at a fixed review budget, does uncertainty-guided correction of machine-generated labels produce better **macro-F1** than random correction? Secondary: How does this differ by baseline classifier and class?

## Pathway and data
**Pathway B - controlled comparative study.** Dataset: **SciCite** (Cohan et al., 2019), citation context classification: **background / method / result**, with author-provided split represented as **8,194 training, 916 validation, 1,859 test** records (HF metadata). Obtain original JSONL archive from https://github.com/allenai/scicite. **Licensing check outstanding:** official repository displays Apache-2.0, but third-party dataset card marks dataset license unknown. Do not redistribute source text until its data terms are confirmed.

## Baselines and fair comparison
Two reproducible CPU-friendly *new* baselines, not replicas of Cohan's neural model: TF-IDF + Logistic Regression; TF-IDF + linear SVM. In each baseline, compare **zero review**, **randomly selected oracle corrections**, and **uncertainty-selected oracle corrections**. Random review repeated with fixed seeds (planned: 20 trials). Review budgets: **5%, 10%, 20%** of held-out items; **10% is primary**. For correction, replace only selected predictions with the dataset reference label, simulating an error-free reviewer. Same predictions, labels, split, and review budget for all strategies. **No real human time, human accuracy, or measured financial cost claims.**

## Metrics, validity and decision rule
**Primary metric:** macro-F1 (higher is better); secondary: accuracy, per-class F1, errors fixed per reviewed item. Success criterion: uncertainty-selected correction yields higher test macro-F1 than the *mean* random-review comparison at the preregistered 10% budget; inspect random-run distribution and uncertainty before interpreting magnitude. Fit preprocessing on train only; use validation for model settings, test once after freezing the protocol. Check duplicate contexts and shared citing/cited-paper identifiers across splits; document any leakage limits. Analyze which classes/errors the selection prioritises.

## Compute, risks and first executable milestone
**Assumption:** Google Colab CPU; exact allocation and timetable are **unknown**. Primary risks: dataset license ambiguity; noisy reference labels; confidence scores not calibrated; possible cross-split paper overlap; simulation overestimating real human review. **Fallback:** use another citation/claim dataset with explicit terms or report the experiment as in-lab-only and omit dataset redistribution, pending instructor confirmation. **First milestone (not yet executed):** download dataset from authors, inspect archive/files, print split sizes/class counts and duplicates, record source version and environment details in genuine Colab logs.

## Evidence sources
- Cohan et al. (2019): SciCite introduces scientific citation-intent data; official data/code repository. https://aclanthology.org/N19-1361/
- Settles (2009): Uncertainty-based query selection is an established active-learning approach; not the same as post-prediction verification. https://minds.wisconsin.edu/handle/1793/60660
- Gilardi et al. (2023): AI-generated annotation can be evaluated against human reference labels; study domain differs from SciCite. https://doi.org/10.1073/pnas.2305016120
- Northcutt et al. (2021): Dataset reference labels can contain errors; findings limit perfect-oracle assumptions. https://doi.org/10.1613/jair.1.12125

**Evidence status:** VERIFIED = assignment/review content and linked original publication/dataset metadata; INFERRED = chosen experimental design; UNKNOWN = dataset-specific reuse permission, student compute/time, feasibility logs, results and novelty beyond this study.
