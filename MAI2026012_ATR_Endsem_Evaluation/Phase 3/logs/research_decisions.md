# Research Decisions and Evidence Ledger — ATR PostMid

**Source context:** Previous literature review titled *Comparing AI-Assisted and Manual Data Labelling Accuracy on Scientific Datasets*, ATR PostMid assignment instructions, and user-reported SciCite experiment outputs.

## Decision log

| Decision | Rationale | Evidence/status | Follow-up |
|---|---|---|---|
| Retain AI-assisted scientific labelling as research area | Continuity with prior literature review required | VERIFIED from supplied review and assignment | Cite the review and primary studies accurately |
| Focus on review-efficiency/accuracy trade-off | Prior review identified unresolved need for system-level cost–accuracy evaluation and selective verification | VERIFIED as a *gap stated in the review*; novel contribution status UNKNOWN | Check neighboring literature before any novelty claim |
| Select SciCite citation-intent classification | Publicly obtainable scientific-text citation context dataset with `background`, `method`, `result` categories | VERIFIED by successful user-reported dataset loading | Confirm data redistribution terms and primary citation |
| Use TF-IDF + Logistic Regression, TF-IDF + Linear SVM | Feasible low-compute transparent comparators | VERIFIED as executed by user in Colab | Preserve exact code and versions |
| Select SVM for oracle correction | Higher cleaned-validation macro-F1 than logistic regression (0.802213 vs 0.791313), with minimal difference in accuracy | VERIFIED via reported Cell 06 output | Do not claim significant superiority |
| Review ranking via two highest LinearSVC scores | Straightforward score-margin uncertainty ranking | VERIFIED as executed in Cell 07 | Explicitly identify this as an uncalibrated margin heuristic |
| Compare to repeated random selection | Baseline for the added value of uncertain-item selection | VERIFIED Cell 08: 100 random runs/selected budget, seed 42 | Retain run-level CSVs |
| Use oracle corrections, not genuine human labels | Feasible, controlled upper-bound comparison without a user study | VERIFIED computational design; human transfer UNKNOWN | Never call these measured human corrections |
| Primary test review budget 100 | A fixed comparison budget after exploratory validation inspection | VERIFIED from chat; **validation-informed, not pre-registered** | Explain explicitly in Methods |
| Exclude validation exact-text overlaps for clean baseline reporting | Two train/validation contexts found | VERIFIED Cells 05–06 | Keep official and cleaned scores distinct |
| Filter test citing-paper overlap for robustness | Shared citing papers may create dependency | VERIFIED Cell 11, 235 examples removed | Identify this as filtered-test sensitivity, not full group-disjoint retraining |

## Research question

At a fixed oracle-correction budget, does selecting uncertain AI-predicted scientific citation labels improve accuracy and macro-F1 more than random selection?

## Implementation study classification

Controlled comparative study with an uncertainty-based selective-correction condition. It is not claimed as a new algorithm, nor as a reproduction of the SciCite source paper.

## Confirmed results from user-shared Colab logs

- Dataset: 8,194 train, 916 validation and 1,859 test records after record-ID deduplication; text field `string`; no missing training text.
- Clean validation (two train-text overlaps removed): LR accuracy 0.827133, macro-F1 0.791313; SVM accuracy 0.828228, macro-F1 0.802213.
- Held-out test, budget 100: baseline accuracy 0.823023, mean random 0.832356, uncertainty 0.850995; oracle corrections found 52/329 initial errors.
- Filtered paper-disjoint test, 1,624 examples, budget 87: baseline 0.816502, mean random 0.826619, uncertainty 0.842980; corrected 43/298 errors.
- Colab Cell 12: evidence export succeeded with 17 files and no missing filenames.

## Uncertainty and limitations

- VERIFIED: Outputs quoted above were provided by the user after local Colab execution; they have not yet been independently rerun or rechecked against the exported files by the assistant.
- INFERRED: Uncertainty-based review likely concentrates incorrect predictions due to lower classification margins. Data directly show a higher error yield at investigated budgets; the mechanism should be phrased cautiously.
- UNKNOWN: Whether real human annotators reproduce the benefits at equivalent time costs, dataset redistribution rights, statistical generality beyond SciCite, novelty relative to all surrounding literature, exact runtime and hardware, and whether a full paper-disjoint retraining protocol would change conclusions.

## Remaining decisions

1. Review actual notebook and exported ZIP for output traceability and environment versions.
2. Decide whether to run an additional clean-train / full-group-disjoint retraining sensitivity experiment.
3. Verify primary sources and data license.
4. Write manuscript with results/limitations separated from earlier literature claims.
5. Publish code and evidence with README, commands and an appropriate data acquisition note, then prepare 5-minute demonstration.
