# Predicting Psychiatric Medication Persistence from EHR Data: Case Study

**Applied Machine Learning Engineer Intern, BRAIV** · Jun–Aug 2026 · Chicago (remote)

> A write-up of my contributions to a team research project at BRAIV, a precision-medicine AI startup. The work used de-identified, IRB-governed records from an academic medical center's research data warehouse. The research is unpublished, so no code, data, schemas, model artifacts or results are shared here.

## The problem

Choosing a psychiatric medication is still largely trial and error. Many patients do not respond to their first medication and cycle through several before one works, which prolongs symptoms and exposes them to side effects. The project explored whether routinely collected EHR data could help predict, before a prescription is written, how likely a patient is to stay on a given psychiatric medication, as an early step toward supporting more individualized treatment selection.

### Persistence is not the same as effectiveness

Standardized symptom scores were recorded for only a small fraction of patients, so the team used **treatment persistence**, whether a patient continued a medication over a clinically meaningful period, as a pragmatic real-world outcome.

This distinction shaped how the work could be interpreted. Persistence captures whether a medication was continued, not whether symptoms improved. A patient may stop a drug because it isn't working, but also because of side effects, cost, access to care, or gaps in follow-up. A model that predicts persistence is therefore not, on its own, a model of which medication works best, and its outputs have to be read with that limitation in mind.

## What I worked on

This was a collaborative project with a multidisciplinary team. The sections below describe the areas I contributed to.

### 1. Understanding the data before modeling it

The project drew on a large, longitudinal, de-identified EHR dataset covering tens of thousands of patients and more than a decade of records, spread across linked tables for demographics, diagnoses, encounters, medications, labs, vitals and social history. I worked with the team on mapping how these tables related to one another, including join keys, the grain of each table and integrity checks. That groundwork made it possible to catch data-quality issues early, before they could distort downstream features.

### 2. Turning prescriptions into treatment episodes

The unit of prediction was a **treatment episode**: a patient paired with a medication, anchored at the start of treatment. Building episodes from raw prescribing records required careful design choices, including standardizing medication names recorded in free text, deciding when separate orders represented one continuous course of treatment, and ensuring that every feature used only information available before treatment began, to prevent leakage.

### 3. Exploring how to compare treatment options

A central question was how a model could compare candidate medications for the same patient rather than simply predicting an outcome for one drug at a time. I contributed to the team's exploration of different modeling strategies for this, weighing trade-offs such as interpretability, data efficiency and how well each approach handled imbalanced data.

### 4. Rigorous evaluation

- **Patient-level separation** between training and evaluation data, so no patient's information leaked across partitions.
- **Calibration and threshold selection** handled separately from final evaluation.
- **Imbalance-aware metrics** covering discrimination, calibration and performance at the chosen operating point.
- **Comparisons across model families,** from linear models to ensembles and neural networks, alongside feature-selection experiments.

### 5. Auditing fairness

The team audited model performance across demographic and coverage-related subgroups. This work shaped how I think about fairness in clinical models, as described in the lessons below.

### 6. Reproducibility and deployment readiness

The pipeline was structured so that every model was trained on a consistent, auditable version of the data. Models were exported as portable artifacts with automated validation, and all computation ran within the institution's secure environment. I also contributed to the study write-up, documenting methods and evaluation design for external review.

## What I learned

These are lessons from exploratory research, not validated findings.

- **Upstream decisions matter enormously.** How a treatment episode is defined, and what counts as the outcome, shaped the results at least as much as the choice of model.
- **Complexity has to earn its place.** This work reinforced the importance of benchmarking sophisticated models against simpler baselines and evaluating whether added complexity translates into meaningful improvements.
- **A model's top features are a question, not an answer.** When strong predictors seem to reflect access to care or engagement with the health system rather than drug response, the next step is to investigate what the model is actually learning before relying on it.
- **Threshold choices can be fairness choices.** When outcome rates differ across groups, a single decision threshold can lead to unequal performance between them, so where to set it deserves deliberate attention rather than a default.

## Tools

Python · pandas · scikit-learn · XGBoost · LightGBM · PyTorch · SHAP · MLflow · HPC

## Data governance

All work used de-identified data under IRB governance, inside the institution's secure computing environment. No patient data, derived datasets, schemas or model artifacts left that environment, and none are included here.

## Contact

Akshaya Ganesh · akshayag00@gmail.com · [LinkedIn](https://www.linkedin.com/)
