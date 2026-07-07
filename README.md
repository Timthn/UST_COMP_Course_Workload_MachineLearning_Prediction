# UST Course Workload Prediction — Project README

This is a machine learning predictive project focusing on the course workloads for Computer Science (COMP) courses at the Hong Kong University of Science and Technology (HKUST). This project aims to address the issue of insufficient course reviews on USTSPACE by building a classification model using online data to assist students in their course selection process.

##  Problem Statement
Course selection is crucial for every student, and they normally rely on USTSPACE to understand the workload and course rating. However, many courses lack sufficient reviews to provide a reliable reference. Our objective is to build a classification model to label the workload rating on a 1-5 scale (representing E to A) or into three bins: High, Medium, and Low, thereby facilitating better course selection.

## Dataset
* **Data Sources**: Raw JSON data was scraped from the UST Space website using Selenium, combined with instructor rating scores from the UST Ranking GitHub repository.
* **Data Scale**: The dataset spans COMP courses from 2016 to 2026, yielding a cleaned dataset of 1,936 observations across 78 courses.
* **Features**: The dataset contains 17 structured variables (e.g., boolean flags for midterm, final, assignments) and 4 text variables (free-text comments).

##  Methodology & Technical Approach
The project evolved through three main phases:
* **Part1 1 (Data Collection & Cleaning)**: We utilized Selenium for scraping, cleaned the data tables, and filtered for English workload text to prepare for subsequent NLP analysis.
* **Part 2 (Baseline Models)**: Initially, we trained One-vs-One (OVO) Logistic Regression, Random Forest, and Decision Tree models using only structured features. Correlation analysis revealed that all structured features had near-zero correlation with the actual workload score, resulting in a baseline accuracy of only about 35.6%.
* **Part 3 (NLP Integration & Model Ensemble)**: We introduced TF-IDF and Truncated SVD to capture the semantics of the English comments. Ultimately, we deployed a Voting Classifier ensemble that combined XGBoost and OVO Logistic Regression.

##  Key Results
* **Accuracy Lift**: By incorporating NLP text features, the 5-class exact match accuracy improved from 35.6% to 43.9%.
* **Binned Performance**: For the three-way binned mapping (High/Medium/Low), the overall accuracy reached 62.5%.
* **Core Insights**: The model is reliable for distinguishing between light and heavy courses, though "medium workload" remains the hardest to predict. The results demonstrate that structural flags alone (like the presence of exams) do not capture how heavy a course feels; fusing structured features with NLP text semantics is essential for reliable predictions.

## Future Work
* Integrate Transformer-based models for more nuanced sentiment analysis.
* Apply lemmatization to extract richer, less redundant TF-IDF terms.

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
or connect via email: thnganaa@connect.ust.hk

---
Last updated: May 2026
