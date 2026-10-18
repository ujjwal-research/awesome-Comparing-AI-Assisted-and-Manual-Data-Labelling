# Baseline Validation Report — ATR PostMid

**Study:** Uncertainty-guided oracle correction for SciCite citation-intent labels  
**Evidence status:** Report of user-provided, genuine Google Colab console outputs; underlying notebooks and exported CSVs have not yet been independently inspected by the assistant.  
**Evaluation date:** October 2026 (specific execution timestamps not recorded)  

## Dataset and protocol

- Source: SciCite public dataset from the authors' SciCite archive (`scicite/train.jsonl`, `scicite/dev.jsonl`, `scicite/test.jsonl`). Downloaded successfully in Colab. Archive SHA-256 as reported by the initial notebook: `711ece2c4e61d116c8ae5bb07e9fbb2ee9ff7bba004b4cab7fbd0ac3af499193`. Verify this against the actual downloaded artifact before treating it as an independently audited checksum.
- JSON field for citation context text: `string`, not `context`; label field: `label`; record key: `unique_id`; cited-paper grouping field used for auditing: `citingPaperId`.
- Record-level de-duplication by `unique_id`: training 8,194; validation 916; test 1,859. Training class counts: background 4,840, method 2,266, result 1,088. No missing training text.
- Feature representation: TF-IDF word unigrams and bigrams, `max_features=20000`.
- Baseline 1: `LogisticRegression(max_iter=1000, random_state=42)`.
- Baseline 2: `LinearSVC(random_state=42)`.
- Training: official training split. Preliminary evaluations: official validation split. Models were **not retrained** between original and cleaned evaluation.

## Confirmed validation results (user-reported Colab outputs)

| Protocol | Baseline | Accuracy | Macro-F1 | N |
|---|---|---:|---:|---:|
| Official validation records | Logistic Regression | 0.827511 | 0.792456 | 916 |
| Official validation records | Linear SVM | 0.828603 | 0.803180 | 916 |
| Exact-context overlap removed from validation | Logistic Regression | 0.827133 | 0.791313 | 914 |
| Exact-context overlap removed from validation | Linear SVM | 0.828228 | 0.802213 | 914 |

Original 916-record SVM confusion matrix (rows true background/method/result; columns predicted background/method/result):

```
[[485, 37, 16],
 [ 68,183,  4],
 [ 29,  3, 91]]
```

This corresponds to 157 misclassifications, of which 68 are true `method` assigned to `background`.

## Data leakage and overlap checks

- Duplicate text within training: 1; within validation: 0; within test: 0. This is separate from duplicates of `unique_id`, which were 0 after cleaning.
- Exact context shared across train/validation: 2; train/test: 0; validation/test: 0.
- Shared citing-paper IDs across train/validation: 468; train/test: 226; validation/test: 59.
- Two train-overlapping contexts were removed **only for the 914-record leakage-controlled validation evaluation**. The official model training data still contained one repeated text with a different record ID. The 914-record validation set still contains citing-paper overlap.
- A sensitivity analysis excluded 235 test examples whose citingPaperId occurred in train, leaving 1,624 examples. This is a **filtered-test robustness analysis**; it does not constitute a full paper-disjoint resplit and retraining.

## Oracle-correction experiment (not human annotation)

Using the trained Linear SVM, rank examples by difference between the two largest `decision_function` class scores. Review budgets are simulated by replacing selected model predictions with existing dataset reference labels. Smaller score margins indicate more ambiguous SVM decisions but are not calibrated probabilities. Under this setup the corrected results are an **oracle upper bound**, assuming reviewers are perfectly accurate. It does not measure reviewer time, effort, actual human errors, or automation bias.

### Held-out test, 1,859 examples, fixed review budget 100

| Strategy | Accuracy | Macro-F1 |
|---|---:|---:|
| No correction | 0.823023 | 0.803991 |
| Random correction (mean over 100 runs, seed 42) | 0.832356 | 0.814303 |
| Uncertainty-guided correction (one deterministic ranking) | 0.850995 | 0.834894 |

- Random-run accuracy SD: 0.002158; this is not a confidence interval.
- Baseline prediction errors: 329. Uncertainty-guided selection corrected 52 errors in 100 reviewed examples.
- **Important data provenance:** primary review budget 100 was selected after examining exploratory validation-budget curves; do not label it pre-registered.

### Filtered paper-disjoint test subset, 1,624 examples, budget 87

| Strategy | Accuracy | Macro-F1 |
|---|---:|---:|
| No correction | 0.816502 | 0.805048 |
| Random correction (mean of 100 runs) | 0.826619 | 0.815844 |
| Uncertainty-guided correction | 0.842980 | 0.833072 |

- 235 test examples removed; 298 baseline errors remain; uncertainty review corrected 43 errors at budget 87.
- The review budget was approximately matched by review percentage (100/1859 vs. 87/1624); absolute budgets differ.

## Validation checks completed

1. Retrieved and parsed the actual JSONL archive after correcting schema errors.
2. Inspected available columns, class labels, split sizes and missing text.
3. Trained two baseline methods with matched TF-IDF representation.
4. Evaluated accuracy, macro-F1, per-class precision/recall/F1, and confusion matrix.
5. Audited exact text overlaps and citing-paper overlap; evaluated on 914-record cleaned validation set.
6. Ran random versus margin-ranked oracle corrections under equal review budgets, including held-out and filtered-test comparisons.
7. Exported 17 files with no missing filenames, as indicated by the user's Cell 12 output.

## Incomplete verification / caveats

- This is a **controlled comparative baseline**, not an exact reproduction of the original neural SciCite publication. No claim of matching its published performance should be made without checking original methodological details.
- Dataset-specific licensing and permitted redistribution need direct confirmation; store an acquisition recipe rather than the dataset itself in a public repository until verified.
- Publication metadata/citation references need primary-source checks before manuscript submission.
- The assistant has not independently rerun the notebook or examined exported CSVs and dependency versions; exact values above are traceable to user-shared console outputs, not independently audited artifacts.
- One repeated training context remains after record-ID deduplication; consider reporting or testing sensitivity to exact-text deduplication when time permits.
- Compare scores within each model using the same preprocessing; do not claim a statistically significant advantage without an appropriate independent inferential design.
- A second independent annotator study is necessary to make empirical claims about manual or hybrid human performance.

## Evidence filenames reported by Colab

`baseline_comparison.csv`, `baseline_clean_results.csv`, `svm_confusion_matrix.png`, `svm_errors.csv`, `train_validation_overlap.csv`, `svm_uncertainty_scores.csv`, `verification_all_runs.csv`, `verification_summary.csv`, `verification_statistics.csv`, `verification_accuracy_curve.png`, `errors_corrected_curve.png`, `heldout_test_results.csv`, `heldout_test_summary.csv`, `paper_disjoint_results.csv`, `paper_disjoint_random_runs.csv`, `environment.json`, `experiment_summary.json`.

## Remaining work

Check the actual notebook and exported data files, secure a copy of the full Colab notebook in `.ipynb` form, document exact dependency versions and run commands, verify paper and dataset provenance, then write a manuscript grounded in these measurements and limitations.
