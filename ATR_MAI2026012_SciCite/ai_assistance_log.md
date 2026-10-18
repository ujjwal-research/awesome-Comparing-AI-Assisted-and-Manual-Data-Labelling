# AI Assistance and Human Verification Log — ATR PostMid

**Scope:** Significant, authentic interactions from the current Colab experiment. Entries distinguish AI suggestions from genuine user execution. Do not interpret drafting a suggested fix as proof that the fix worked until the user's subsequent console output confirms it.

| Stage | AI-assisted proposal / observed issue | Human action / actual evidence | Correction or decision | Verification status |
|---|---|---|---|---|
| First attempt to load SciCite | Assistant incorrectly referred to text column as `context` and assumed archive parsing would work | User ran Cell 1; Pandas raised `KeyError: Index(['context'], dtype='object')` | Diagnose column mismatch, not a missing archive | VERIFIED error from user traceback |
| Unsuccessful debugging iteration | Assistant wrongly attributed the error to selecting auxiliary scaffold training files | User printed archive filenames, which included both main `train.jsonl` and scaffold data; selecting main file still produced same `KeyError` | Previous diagnosis withdrawn; need inspect actual JSON schema | VERIFIED failed fix from user traceback |
| Successful loading | Assistant corrected text field to `string` and deduplicated by `unique_id` | User reported train=8194, validation=916, test=1859, all expected fields including `string`; no missing text | Main dataset loading was successful | VERIFIED user-reported console output |
| Logistic Regression baseline | Assistant supplied TF-IDF + Logistic Regression code | User executed it and reported accuracy 0.827510917 and macro-F1 0.792456190 on 916-record validation | Keep as baseline comparator | VERIFIED user-reported console output |
| Linear SVM baseline | Assistant supplied matched TF-IDF + LinearSVC code | User reported accuracy 0.828602620 and macro-F1 0.803179861 | Provisionally selected SVM due to better validation macro-F1 | VERIFIED user-reported console output |
| SVM error inspection | Assistant supplied confusion-matrix and per-item error reporting | User shared 3-class confusion matrix and count of 157 errors | Recognized method→background confusion (68 cases) | VERIFIED user-reported image/data |
| Overlap audit | Assistant supplied dataset overlap auditing cell | User found one duplicate training text, 2 shared train–validation contexts, 468 shared train–validation citing-paper IDs, 226 shared train–test citing-paper IDs | Added exact-text removal in validation, paper-overlap caveat | VERIFIED user-reported output |
| Clean validation | Assistant supplied filtered evaluation without retraining | User reported clean validation n=914 and LR/SVM metrics 0.827133/0.791313 and 0.828228/0.802213 | Preserve official and leakage-controlled figures separately | VERIFIED user-reported output |
| Uncertainty ranking | Assistant proposed top-two class score margin | User reported 914 examples, 157 errors; 4 errors among 10 smallest margins | Proceed to matched-budget oracle comparison | VERIFIED user-reported output |
| Random versus uncertain oracle review | Assistant supplied comparison over budgets with 100 seeded random runs | User reported uncertainty outperforming random at all nonzero validation budgets | Retain validation exploration; do not claim actual human performance | VERIFIED user-reported output |
| Statistical curves | Assistant supplied exports and plotted curves | User supplied tables and figures; at budget 100 uncertainty selected 43 errors vs random mean 16.83 | Interpretation as error-enrichment in review queue | VERIFIED user-reported output |
| Held-out evaluation | Assistant supplied fixed 100-review test cell | User reported 1,859 test examples, baseline accuracy 0.823023, random mean 0.832356, uncertain 0.850995, 52 errors corrected | Treat as held-out **oracle-simulation** result, not human study | VERIFIED user-reported output |
| Paper-overlap sensitivity | Assistant supplied citing-paper filtered test analysis | User reported 1,624 examples, budget 87, uncertain accuracy 0.842980 vs random 0.826619 | Describe as filtered-test sensitivity, not full paper-disjoint retraining | VERIFIED user-reported output |
| Evidence export | Assistant supplied ZIP packaging cell | User reported `ATR_Experimental_Evidence.zip`, 17 files, `Missing files: []` | Package created on user's Colab session; assistant has not directly inspected it | VERIFIED completion message; contents not independently inspected |

## Reflection / integrity notes

1. **AI error surfaced through execution:** The model hallucinated or guessed a `context` field rather than inspecting schema. The real field was `string`.
2. **Initial diagnosis was incorrect:** Auxiliary scaffold filenames were present, but did not explain the `context` KeyError when the correct main file was selected. The user reran and falsified that explanation.
3. **Design decision requiring human oversight:** The review budget of 100 was fixed for held-out testing after examining validation results, so it must be described as validation-informed, not prospectively registered.
4. **Scientific limitation:** Reference-label substitution represents a perfect oracle, not measured human review; claims must distinguish them.
5. **Reproducibility limitation:** User-shared logs support the recorded measurements, but an independent rerun from the exported notebook and archived files remains outstanding.

## User tasks before submission

- Retain the actual `.ipynb` notebook, complete traceback(s) if still present, CSVs, generated figures, and ZIP.
- Add genuine dates, Colab runtime mode, installed package versions and any independently performed checks; do not guess them.
- Confirm prompts and corrections accurately reflect actual execution history. If any item is inaccurate, amend the log.
- Record additional **real** manual interventions only if they occurred.

**AI-use disclosure draft:** AI assistance was used to propose research framing, Python code, debugging steps, evaluation design, interpretation guidance, and documentation. The student executed the Colab cells, inspected failures, returned genuine outputs, and selected/verified necessary corrections. Results reported here derive from user-executed code, not from AI-invented metrics.
