# Phase 3 - Prompts 08-11

This folder contains Phase III documentation and evidence from the executed SciCite Colab notebook.

- `Phase 3.pdf`: combined prompts 08-11 report.
- `Prompt 08.pdf` to `Prompt 11.pdf`: standalone prompt-by-prompt reports.
- `notebooks/ATR_EndSem.ipynb`: the executed notebook (Cells 01-12, with Phase III baseline work in Cells 01-06).
- `results/`: actual baseline metrics, confusion matrix, errors, overlap audit and environment metadata.
- `logs/`: baseline validation, authentic AI debugging and research decisions.
- `requirements.txt`: recorded core environment versions; requests/matplotlib versions not recorded, so left unpinned.

## Reproduction

Open the notebook in Google Colab, run its cells in order, and verify the dataset dimensions 8194/916/1859. The notebook downloads SciCite from the original dataset archive. Check dataset terms before redistributing raw data. Baseline comparison uses 914 validation examples after removing two exact train-validation text overlaps. A clean independent runtime reproduction has not yet been documented.

## Integrity

The TF-IDF classifiers are lightweight baselines, not a faithful reproduction of the original SciCite neural model. The notebook's later uncertainty correction experiments are preserved for future phases; the current report covers environment, baseline implementation, validation and debugging. The initial later-stage JSON summary had a reused-variable defect; the correct held-out macro-F1 was 0.803991, as recorded in the genuine held-out CSV.
