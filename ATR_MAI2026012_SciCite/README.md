# SciCite uncertainty-guided oracle label verification

This folder contains the implementation study continuing an earlier literature review comparing AI-assisted and manual scientific-data labelling. It is **not** an experiment with human reviewers. Reference labels are used to simulate perfect review corrections (oracle upper bound).

## Main outputs (recorded Colab run)

| Set | SVM baseline accuracy | Mean random correction | Uncertainty correction | Budget |
|---|---:|---:|---:|---:|
| Validation after removing exact context overlaps (n=914) | 0.828228 | 0.846641 | 0.875274 | 100 |
| Held-out test (n=1859) | 0.823023 | 0.832356 | 0.850995 | 100 |
| Paper-filtered test subset (n=1624) | 0.816502 | 0.826619 | 0.842980 | 87 |

Random results average 100 random draws; all corrections assume perfect knowledge of reference labels. No statistical significance claim is made.

## Files

- `notebooks/ATR_EndSem.ipynb`: actual executed Colab notebook containing Cell 01–12 in order
- `results/`: genuine CSVs, PNGs, `environment.json`, and the original summary export
- `paper/main.tex`, `paper/references.bib`, `paper/figures/`: Overleaf source
- `paper/Overleaf_Paper.pdf`: compiled paper uploaded after Overleaf compilation
- `research_brief.md`: G1 research brief
- `baseline_validation.md`, `research_decisions.md`, `ai_assistance_log.md`: research provenance

## How to reproduce

1. Open Google Colab and upload `notebooks/ATR_EndSem.ipynb`.
2. Run the notebook code cells in order. It downloads SciCite from `https://s3-us-west-2.amazonaws.com/ai2-s2-research/scicite/scicite.tar.gz`. Check data-use terms before redistributing raw data. The dataset is not stored in this repository.
3. Check split sizes (train 8194, validation 916, test 1859), training fields (`string`, `label`, `unique_id`), and the context-overlap audit.
4. Record the environment versions; the Colab run used Python 3.13.16, numpy 2.1.3, pandas 2.2.3 and scikit-learn 1.6.1. `requirements.txt` records those versions; `requests` and `matplotlib` versions were not recorded and are **not** pinned. A clean re-run on a different environment is **not yet independently verified**.
5. Execute both baselines, the uncertainty selection, 100 random repetitions at seed 42, held-out evaluation, and paper-filtered subset evaluation. Compare fresh results against the CSV files in `results/`.
6. For the paper, upload the `paper/` folder as an Overleaf project or compile `main.tex` with a LaTeX installation including BibTeX.

## Method and limitations

TF-IDF uses unigram/bigram features (up to 20,000); models are Logistic Regression and LinearSVC. Low top-two SVM decision-score margin determines review priority. Baselines are trained on the official training split. Two exact train-validation shared texts are excluded from the cleaned validation evaluation. Test subset sensitivity excludes examples whose `citingPaperId` occurs in training. This is not complete group-disjoint retraining.

# SciCite uncertainty-guided oracle label verification

This folder contains the implementation study continuing an earlier literature review comparing AI-assisted and manual scientific-data labelling. It is **not** an experiment with human reviewers. Reference labels are used to simulate perfect review corrections (oracle upper bound).

## Main outputs (recorded Colab run)

| Set | SVM baseline accuracy | Mean random correction | Uncertainty correction | Budget |
|---|---:|---:|---:|---:|
| Validation after removing exact context overlaps (n=914) | 0.828228 | 0.846641 | 0.875274 | 100 |
| Held-out test (n=1859) | 0.823023 | 0.832356 | 0.850995 | 100 |
| Paper-filtered test subset (n=1624) | 0.816502 | 0.826619 | 0.842980 | 87 |

Random results average 100 random draws; all corrections assume perfect knowledge of reference labels. No statistical significance claim is made.

## Files

- `notebooks/ATR_EndSem.ipynb`: actual executed Colab notebook containing Cell 01–12 in order
- `results/`: genuine CSVs, PNGs, `environment.json`, and the original summary export
- `paper/main.tex`, `paper/references.bib`, `paper/figures/`: Overleaf source
- `paper/Overleaf_Paper.pdf`: compiled paper uploaded after Overleaf compilation
- `research_brief.md`: G1 research brief
- `baseline_validation.md`, `research_decisions.md`, `ai_assistance_log.md`: research provenance

## How to reproduce

1. Open Google Colab and upload `notebooks/ATR_EndSem.ipynb`.
2. Run the notebook code cells in order. It downloads SciCite from `https://s3-us-west-2.amazonaws.com/ai2-s2-research/scicite/scicite.tar.gz`. Check data-use terms before redistributing raw data. The dataset is not stored in this repository.
3. Check split sizes (train 8194, validation 916, test 1859), training fields (`string`, `label`, `unique_id`), and the context-overlap audit.
4. Record the environment versions; the Colab run used Python 3.13.16, numpy 2.1.3, pandas 2.2.3 and scikit-learn 1.6.1. `requirements.txt` records those versions; `requests` and `matplotlib` versions were not recorded and are **not** pinned. A clean re-run on a different environment is **not yet independently verified**.
5. Execute both baselines, the uncertainty selection, 100 random repetitions at seed 42, held-out evaluation, and paper-filtered subset evaluation. Compare fresh results against the CSV files in `results/`.
6. For the paper, upload the `paper/` folder as an Overleaf project or compile `main.tex` with a LaTeX installation including BibTeX.

## Method and limitations

TF-IDF uses unigram/bigram features (up to 20,000); models are Logistic Regression and LinearSVC. Low top-two SVM decision-score margin determines review priority. Baselines are trained on the official training split. Two exact train-validation shared texts are excluded from the cleaned validation evaluation. Test subset sensitivity excludes examples whose `citingPaperId` occurs in training. This is not complete group-disjoint retraining.

**Evidence correction:** The original `results/experiment_summary.json` erroneously records `test_baseline_macro_f1` as 0.805048 (a later paper-filtered value), due to variable reuse. The true held-out value is **0.803991** from `results/heldout_test_summary.csv`. The source export is retained unchanged for provenance.

No human annotators participated and no reviewer time, cost or inter-rater accuracy was measured. The paper's results are limited to this dataset and correction simulation. License terms for raw SciCite records should be independently verified.

No human annotators participated and no reviewer time, cost or inter-rater accuracy was measured. The paper's results are limited to this dataset and correction simulation. License terms for raw SciCite records should be independently verified.
