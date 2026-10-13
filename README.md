# Synthetic COVID-19 Triage Risk Prediction Using Radiomics, Clinical and Laboratory Features

> **Academic prototype only:** This project uses a synthetically generated dataset. It does not use the original patient-level data or real CT images from the reference paper. Results are not clinically validated and must not be used for patient-care decisions.

## Overview

This mini-project builds a machine-learning workflow inspired by **“CT-based Patient Triage of COVID-19: Radiomics Prediction of ICU Admission, Mechanical Ventilation, and Death of Patients”** by Xianghao Zhan and Yiheng Li.

The project explores three binary outcomes:
- ICU admission (`ICU`)
- Mechanical ventilation (`mechanical_ventilation`)
- Death (`death`)

The original patient-level dataset was not used. Instead, a synthetic dataset was generated for educational experimentation. Radiomics-style columns are simulated numeric features, not features extracted from actual CT scans.

## Objectives

1. Validate and explore a synthetic tabular dataset.
2. Compare radiomics-only, radiomics-plus-clinical, and radiomics-plus-clinical-and-laboratory feature groups.
3. Apply preprocessing and categorical encoding.
4. Explore training-data class-imbalance handling with SMOTEENN.
5. Apply LASSO-based feature selection.
6. Train five machine-learning classifiers.
7. Evaluate using accuracy, precision, recall, F1-score, ROC-AUC, and PR-AUC.
8. Examine model behaviour with feature-importance analysis.
9. Document limitations and reproducibility.

## Dataset

The synthetic dataset contains **2,400 rows and 155 columns**:
- Patient identifier: `patient_id`
- Demographics, symptoms, and comorbidities
- 17 simulated laboratory variables
- 120 simulated radiomics-style features
- Three target columns: `ICU`, `mechanical_ventilation`, and `death`

Radiomics-style feature families are labelled first-order, GLCM, GLSZM, GLRLM, NGTDM, and wavelet. These are synthetic numerical columns and are not derived from medical images.

Expected data files:
- `data/synthetic_covid_dataset.csv`
- `data/data_dictionary.csv`

## Feature Groups

| Group | Contents |
|---|---|
| `Radiom` | Radiomics-style features |
| `RadioClin` | Radiomics-style and clinical features |
| `RadioClinLab` | Radiomics-style, clinical, and laboratory features |

Categorical encoding can increase the number of columns in the processed matrices.

## Workflow

Update notebook names to match the actual repository files.

1. `01_dataset_validation.ipynb` — dataset validation
2. `02_eda.ipynb` — exploratory data analysis
3. `03_preprocessing.ipynb` — preprocessing experiments
4. `04_feature_groups.ipynb` — feature-group construction
5. `05_class_imbalance.ipynb` — SMOTEENN on training data
6. `06_lasso_feature_selection.ipynb` — LASSO feature selection
7. `07_model_training.ipynb` — classifier training
8. `08_model_evaluation.ipynb` — metrics, ROC/PR curves, confusion matrices
9. `09_feature_importance.ipynb` — permutation importance
10. `10_final_results.ipynb` — final comparison summary

## Models

- Logistic Regression
- Random Forest
- Support Vector Machine (SVM)
- Multi-Layer Perceptron (MLP)
- LightGBM

The comparison contains 45 evaluations: 3 feature groups × 3 targets × 5 classifiers.

## Current Top Results

These are the top rows supplied from the current model comparison. Verify each is the highest ROC-AUC row across all 45 evaluations before describing it as the definitive best model for that target.

| Target | Feature group | Model | Accuracy | Precision | Recall | F1-score | ROC-AUC | PR-AUC |
|---|---|---|---:|---:|---:|---:|---:|---:|
| ICU admission | RadioClinLab | Logistic Regression | 0.321 | 0.301 | 1.000 | 0.463 | 0.721 | 0.509 |
| Death | RadioClinLab | Random Forest | 0.200 | 0.172 | 1.000 | 0.294 | 0.730 | 0.317 |
| Mechanical ventilation | RadioClinLab | Logistic Regression | 0.343 | 0.308 | 0.967 | 0.467 | 0.737 | 0.552 |

### Interpretation

The listed results show high recall but low accuracy and precision, suggesting many cases may be classified as positive at the current threshold. Review confusion matrices, threshold-dependent trade-offs, calibration, and validation performance. Select models using validation data where possible; selecting the best model on test-set metrics can produce optimistic estimates.

## Metrics

- **Accuracy:** proportion of all predictions that are correct.
- **Precision:** proportion of predicted positives that are true positives.
- **Recall:** proportion of actual positives identified.
- **F1-score:** harmonic mean of precision and recall.
- **ROC-AUC:** ranking performance across classification thresholds.
- **PR-AUC / Average Precision:** summary of precision-recall performance, useful with imbalanced targets.

## Limitations and Ethical Use

- Data is synthetic and may not reflect real clinical distributions or relationships.
- No original patient-level cohort, real CT images, or segmentation masks were used.
- Radiomics-style columns are simulated, not image-derived.
- Metrics depend on the synthetic generator and the split.
- Feature importance is model-dependent and does not prove causation or medical significance.
- This is an educational prototype, not a reproduction or clinical validation of the reference paper.
- Do not use the outputs for diagnosis, triage, or treatment.

## Reproducibility

1. Use Google Colab or a compatible Python environment.
2. Install the notebook dependencies: `numpy`, `pandas`, `scikit-learn`, `imbalanced-learn`, `matplotlib`, `seaborn`, `joblib`, and `lightgbm`.
3. Put the synthetic dataset and data dictionary in the expected `data/` directory.
4. Run notebooks in pipeline order and update paths for your environment.
5. Keep resampling and learned preprocessing confined to training data.
6. Record package versions and random seeds for the final submission.

## Reference

Zhan, X. and Li, Y. “CT-based Patient Triage of COVID-19: Radiomics Prediction of ICU Admission, Mechanical Ventilation, and Death of Patients.”

## Disclaimer

This project is for coursework and machine-learning education only. It does not provide clinically validated predictions.
