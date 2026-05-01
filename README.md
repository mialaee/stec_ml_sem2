# stec_ml_sem2
Applied Data Science in Biology Semester 2 assessment 2026

# STEC Geographical Source Attribution Using K-mer Profiles

This project uses Random Forest machine learning models to predict the geographical origin of Shiga-toxigenic *Escherichia coli* (STEC) isolates from genome-wide k-mer profiles.

The analysis compares country-level and region-level source attribution, evaluates the effect of feature selection and balancing strategies, and tests a hierarchical region-country prediction approach.

# Project Overview

The main aims were to:

- Build baseline Random Forest models for country and region prediction.
- Assess the effect of class imbalance on model performance.
- Compare different k-mer feature-set sizes, including 3,000, 5,000, 10,000, 20,000, 30,000, 40,000 and 50,000 selected features.
- Test balancing strategies including no resampling, UK undersampling, majority-class undersampling and hybrid resampling.
- Compare tuned Random Forest models with baseline models.
- Test a hierarchical model that predicts region first and then country.
- Evaluate models using accuracy, balanced accuracy, macro precision, macro recall, macro F1-score, weighted F1-score and Matthews correlation coefficient.
- Generate confusion matrices, feature-size trend plots and feature importance plots.

# Repository Structure

```text
.
├── stec_notebook.ipynb
├── README.md
├── data/
│   ├── 14-18kmerdata.txt
│   ├── 19kmerdata.txt
│   ├── 14-18metadata
│   └── 19metadata
└── outputs/
    ├── figures/
    ├── tables/
    └── models/
```

# Data

The raw data files are not included in this repository because they were provided for assessment use and may be too large or restricted.

To run the notebook, users should create a folder called `data/` in the same directory as `final_stec.ipynb` and place the following files inside it:

- `14-18kmerdata.txt`
- `19kmerdata.txt`
- `14-18metadata`
- `19metadata`

The notebook expects these exact filenames. If the files are stored somewhere else, the file paths in the loading section of the notebook must be updated.

# Main Notebook

The full analysis is contained in:

stec_notebook.ipynb

The notebook performs the following steps:

1. Imports packages and creates output folders.
2. Loads k-mer matrices and metadata.
3. Cleans and standardises metadata labels.
4. Aligns train and test k-mer matrices.
5. Builds baseline country and region Random Forest models.
6. Generates baseline classification reports and confusion matrices.
7. Runs country and region model comparison grids.
8. Tests feature-set sizes from 3,000 to 50,000 k-mers.
9. Tests different balancing strategies and Random Forest settings.
10. Selects the best country and region models using balanced accuracy, macro F1-score and MCC.
11. Builds and evaluates a hierarchical region-country model.
12. Saves final tables, figures and model outputs.

# Outputs

The notebook creates the following output folders:

outputs/figures/
outputs/tables/
outputs/models/

Key outputs include:

- Dataset summary table.
- Baseline model comparison table.
- Best model settings table.
- Final model comparison table.
- Country and region class distribution plots.
- Original country and region confusion matrices.
- Tuned country and region confusion matrices.
- Hierarchical model confusion matrix.
- Feature-size performance trend plots.
- Multi-panel model comparison plot.
- Top k-mer feature importance plots.

# Model Evaluation

The models were evaluated using:

- Accuracy.
- Balanced accuracy.
- Macro precision.
- Macro recall.
- Macro F1-score.
- Weighted F1-score.
- Matthews correlation coefficient.
- Confusion matrices.

Balanced accuracy, macro F1-score and MCC were prioritised because the dataset was strongly imbalanced. Accuracy alone was not sufficient because high accuracy could be driven by correct prediction of majority classes, particularly the UK class.

# Key Findings

The original country model had moderate accuracy but very low balanced accuracy and macro F1-score, showing strong bias towards the dominant UK class.

The tuned country model improved class-wise performance after feature selection and UK undersampling. The best country model used 30,000 selected k-mers.

The tuned region model achieved the strongest balanced accuracy and macro F1-score overall. The best region model used 50,000 selected k-mers and hybrid balancing.

The hierarchical region-country model improved over the original country model but did not outperform the best tuned flat country model, suggesting that error propagation from the first-stage region prediction limited its usefulness.

# Requirements

The analysis was run in Python using:

pandas
numpy
matplotlib
scikit-learn

Install dependencies using:

pip install -r requirements.txt

A minimal `requirements.txt` file should contain:

pandas
numpy
matplotlib
scikit-learn

# Notes

The `data/` folder should be excluded from GitHub if the raw files are large, restricted or provided only for assessment use.

The trained model files in `outputs/models/` may also be excluded because they can be regenerated by running the notebook.

Recommended `.gitignore` entries:

data/
outputs/models/
.ipynb_checkpoints/
__pycache__/
*.pkl

# Author

Mia
