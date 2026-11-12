# Week 17: Classifier Comparison

**Result:** The Decision Tree had the highest mean three-fold training cross-validation average precision (0.2086). On the fixed test split, its average precision was 0.1958 versus 0.1126 for a constant-score prevalence baseline; its accuracy was 0.6548 versus 0.8874 for the majority-class baseline. This is retrospective model evidence, not a promise of business lift.

## Quick start

1. Open the [working notebook](prompt_III_working.ipynb) in Jupyter.
2. Start Jupyter from the repository root so the notebook's relative CSV path resolves.
3. Keep the [Bank Marketing CSV](data/bank-additional-full.csv) under `data/`. The [companion paper](https://www.researchgate.net/publication/236231158_Using_Data_Mining_for_Bank_Direct_Marketing_An_Application_of_the_CRISP-DM_Methodology) is available online and is not required to run the notebook.
4. Install the runtime dependencies in your own environment, then run the notebook from top to bottom:

   ```powershell
   python -m pip install jupyterlab pandas numpy scipy scikit-learn matplotlib seaborn
   jupyter lab prompt_III_working.ipynb
   ```

## Model results

Hyperparameters were selected using average precision on three stratified folds of the training set only. Preprocessing was fitted inside each cross-validation pipeline; the same held-out test split was used only for final evaluation.

| Model | Mean CV average precision | Test average precision | Test accuracy |
|---|---:|---:|---:|
| Decision Tree | 0.2086 | 0.1958 | 0.6548 |
| Logistic Regression | 0.2049 | 0.1888 | 0.8874 |
| SVM | 0.1972 | 0.1818 | 0.6272 |
| KNN | 0.1856 | 0.1750 | 0.8860 |

The higher-AP models trade away majority-class accuracy at their default prediction threshold. Average precision evaluates ranking quality; it does not by itself define an operational threshold or establish causal impact.

## Data and scope

The notebook uses the public `bank-additional-full.csv` Bank Marketing variant from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/bank+marketing), based on contacts from a Portuguese banking institution. The accompanying Moro, Laureano, and Cortez paper is linked above. The target is subscription (`y`). Modeling and EDA use seven pre-call fields: age, job, marital status, education, credit default, housing loan, and personal loan. Call duration is excluded because it is only available after a contact. Literal `unknown` values are retained as categories; the selected fields contain no nulls and no imputation is used.

## Recommended next step

Assess the model in a controlled, fixed-capacity pilot randomized against current calling practice. Track subscribers per 100 calls and precision among contacts reached at capacity; check performance over time and across relevant customer groups before any rollout.
