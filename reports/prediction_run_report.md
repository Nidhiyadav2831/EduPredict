# EduPredict — Prediction Execution Run Report

> **Dataset Notice:** All predictions were generated for **synthetic student records** (`data/student-mat-synthetic.csv` stored in MongoDB `edupredict_db.students`).  
> **Predictive Disclaimer:** Predictions represent **statistical estimates** based solely on non-grade demographic, lifestyle, and behavioral factors; they do **not** constitute real-world academic evaluations or guarantees of future academic standing.

---

## 1. Run Execution Metadata

| Attribute | Details |
|---|---|
| **Execution Date & Time** | `2026-10-29 13:56:29 UTC` |
| **Model Version** | `v1` |
| **Model Artifacts Used** | `decision_tree_classifier.joblib, random_forest_classifier.joblib, random_forest_regressor.joblib` |
| **Database & Collection** | `edupredict_db.student_predictions` |
| **Input Features Evaluated** | **30 features** (Grade columns G1, G2, G3 strictly excluded) |

---

## 2. Processing Summary

| Processing Metric | Count |
|---|---|
| **Total Records Attempted** | **10** |
| **Successful Predictions** | **10** (100.0%) |
| **Failed Records** | **0** |
| **MongoDB Upserted Records** | **10** |
| **MongoDB Matched / Updated Records** | **0** |

---

## 3. Sample Scored Predictions (First 10 Records)

| Student ID | Row ID | Decision Tree Risk | Random Forest Risk | RF Risk Probability | Estimated G3 (0–20) |
|---|---|---|---|---|---|
| `6ae34f2432799e52f3e0592c` | 1 | Passing | Passing | 27.3% | 9.75 |
| `6ae34f2432799e52f3e0592d` | 2 | At-Risk | Passing | 39.7% | 9.89 |
| `6ae34f2432799e52f3e0592e` | 3 | Passing | Passing | 42.4% | 9.48 |
| `6ae34f2432799e52f3e0592f` | 4 | At-Risk | At-Risk | 63.1% | 9.81 |
| `6ae34f2432799e52f3e05930` | 5 | Passing | Passing | 28.9% | 9.19 |
| `6ae34f2432799e52f3e05931` | 6 | Passing | Passing | 36.2% | 10.78 |
| `6ae34f2432799e52f3e05932` | 7 | At-Risk | At-Risk | 53.1% | 11.24 |
| `6ae34f2432799e52f3e05933` | 8 | Passing | Passing | 42.8% | 7.99 |
| `6ae34f2432799e52f3e05934` | 9 | At-Risk | At-Risk | 63.8% | 8.82 |
| `6ae34f2432799e52f3e05935` | 10 | Passing | Passing | 49.8% | 8.89 |

---

## 4. Error & Validation Diagnostics

None (All records scored successfully).

---

## 5. Architectural Safeguards

- **Zero Target Leakage:** Features `G1`, `G2`, `G3`, and `at_risk` were stripped prior to prediction; inference was conducted strictly on non-grade attributes.
- **Idempotency Confirmed:** MongoDB predictions collection uses a compound upsert filter on `(student_id, model_version)`, ensuring duplicate executions update records cleanly in-place without data duplication.
- **Source Integrity Preserved:** Original documents in `edupredict_db.students` were accessed read-only with zero modifications.
