# UST Course Workload Prediction — Project README

## Overview
This repository contains the analysis pipeline and notebooks used to collect, clean, feature-engineer, and model student course reviews from UST (University) to predict perceived course workload. The project workflow is split into three stages: web scraping, data cleaning, and modeling (including NLP sentiment features).

## Repository Structure (high level)
- `1.USTSPACE_web_scrab.ipynb` — Web scraping and raw data collection into `ust_reviews/`.
- `2.*` notebooks — Data cleaning and consolidation into cleaned datasets under `ust_review_cleanned_baseline/` and `ust_review_cleanned_with_review*/`.
- `3.*` notebooks — Feature engineering and modeling (workload prediction) using cleaned datasets.
- `ust_reviews/` — Raw scraped JSON/CSV files (input to cleaning notebooks).
- `ust_review_cleanned_baseline/`, `ust_review_cleanned_with_review/`, `ust_review_cleanned_with_reviews_10yrs/`, `ust_review_cleanned_with_reviews_10yrs_no_instructor_dropping/` — Processed datasets and per-course folders with cleaned CSVs.

## Key Notebooks
- [1.USTSPACE_web_scrab.ipynb](1.USTSPACE_web_scrab.ipynb) — Scrapes course reviews and saves raw data to `ust_reviews/`.
- [2.ieda3560_project_data_cleaning.ipynb](2.ieda3560_project_data_cleaning.ipynb) — Core cleaning pipeline that produces baseline cleaned outputs.
- [2.Group7_UST_course_workload_prediction_data_cleaning.ipynb](2.Group7_UST_course_workload_prediction_data_cleaning.ipynb) — Group notebook for cleaning and assembling the dataset used for modeling.
- [3.Group7 _UST_course workload prediction_script_modeling.ipynb](3.Group7 _UST_course workload prediction_script_modeling.ipynb) — Feature engineering (including text sentiment/NLP features) and model training/evaluation.


## Data
- Raw source: `ust_reviews/` (outputs from the scraping notebook).
- Cleaned outputs: CSV files in `ust_review_cleanned_baseline/` and the `ust_review_cleanned_with_review*` folders. The consolidated cleaned file `all_courses_cleaned.csv` is present in those folders and is the primary input for modeling.

## How the pipeline flows
1. Run the scraper notebook to populate `ust_reviews/` (if you need fresh data).
2. Run the data cleaning notebooks (`2.*`) to transform raw review records into a tabular CSV dataset (deduplication, normalization, review/text cleaning, filtering to desired years/instructors as needed).
3. Run the modeling notebook (`3.*`) to extract features (text sentiment, review counts, course metadata), train predictive models, and evaluate performance.

## Quick start — recommended order
1. Open `1.USTSPACE_web_scrab.ipynb` to inspect raw collection (skip if you already have `ust_reviews/`).
2. Open and run `2.Group7_UST_course_workload_prediction_data_cleaning.ipynb` to produce the cleaned dataset used in experiments.
3. Open and run `3.Group7 _UST_course workload prediction_script_modeling.ipynb` to reproduce modeling results.

## Dependencies
- Python 3.8+ recommended
- Typical packages used across notebooks: `pandas`, `numpy`, `scikit-learn`, `nltk` or `spacy`, `matplotlib`/`seaborn`, `jupyter`/`notebook`, and any transformer or sentiment libraries used in notebook cells. Install with pip as needed:

```powershell
pip install pandas numpy scikit-learn jupyter matplotlib seaborn nltk spacy
```

Adjust the list per the `import` cells at the top of each notebook.

## Outputs & Results
- Model evaluation metrics and plots are recorded inside the modeling notebooks (see the last sections of the `3.*` notebooks).
- Cleaned CSV outputs (including `all_courses_cleaned.csv`) live in the `ust_review_cleanned_*` folders.

## Notes & recommendations
- Check the top cells of each notebook for required environment setup (token/API keys for scraping, NLTK downloads, etc.).
- Notebooks are written to be run interactively — run cells in order and restart the kernel between major changes.

## Contact / Authors
Group 7 — Project for IEDA3560. For questions, open an issue or contact the project authors listed in the notebook headers.

---
Last updated: May 2026
