# IMDb Genre Classification with Naive Bayes and Comparative Models

## Project overview

This project studies the prediction of a movie's **main genre** from structured numerical features extracted from a large IMDb-style dataset.

The initial academic objective was to use a **Naive Bayes** classifier to predict the genre of a film.  
To strengthen the analysis and reach a more rigorous engineering-level methodology, the project was extended with:
- a full data preparation pipeline,
- feature engineering,
- class reduction to the most represented genres,
- and a comparative evaluation against other machine learning models.

The final goal is not only to train a classifier, but also to understand:
- how data quality impacts performance,
- how preprocessing decisions affect learning,
- and how different model families behave on the same classification problem.

---

## Problem statement

We aim to predict the **main genre** of a movie using the following structured variables:

- `year`
- `rating`
- `duration`
- `votes`
- `gross_income`
- `certificate`

Because the raw dataset contains noisy, heterogeneous and partially unstructured fields, a substantial preprocessing phase is required before training any model.

---

## Dataset

The source dataset is from : "https://www.kaggle.com/datasets/ashishjangra27/imdb-movies-dataset" and is stored in:

data/raw/movies.csv

### Main columns used in the project:

- year — release year information
- rating — movie rating
- certificate — audience certification
- duration — movie duration
- genre — movie genre
- votes — number of votes
- gross_income — gross income

### Main data issues identified

During preprocessing, several issues were detected:

year values were not stored as plain numeric years and contained patterns such as (2015 TV Special)
duration contained text values such as 94 min
votes contained separators and mixed formats
gross_income contained heterogeneous formats, including values such as 1,000,000 and $0.01M
genre sometimes contained multiple labels
some classes were very rare and would destabilize training

These issues motivated a full cleaning and normalization pipeline.

## Methodology
1. Data preprocessing
2. Feature selection
3. Genre encoding
4. Train/test split
5. Model training (GaussianNB)
6. Evaluation (accuracy, precision, recall, F1-score)

##  Project Structure
```t
imdb-genre-naive-bayes/
├── data/
│   ├── raw/
│   │   └── movies.csv
│   └── processed/
├── notebooks/
│   ├── 01_preparation_donnees.ipynb
│   └── 02_entrainement_modeles.ipynb
├── models/
├── reports/
├── .gitignore
├── requirements.txt
└── README.md
```

## Workflow
### Notebook 1 — Data preparation

The first notebook focuses on turning the raw dataset into a clean and model-ready dataset.

Main steps:

- project path definition using Path
- raw data loading
- column selection
- data type normalization
- cleaning of year, duration, votes, and gross_income
- extraction of the main genre
- filtering to the top N most represented genres
- logarithmic transformation of skewed numerical variables
- encoding of categorical variables
- export of the final processed dataset

Output files:

data/processed/movies_clean.csv
data/processed/genre_label_mapping.csv

### Notebook 2 — Model training and evaluation

The second notebook focuses on supervised learning and comparison of models.

Main steps:

- loading the processed dataset
- definition of features and target
- train/test split with stratification
- model training
- evaluation using several metrics
- confusion matrices
- per-class performance analysis
- model comparison

Models compared:

- Gaussian Naive Bayes
- Random Forest
- Gradient Boosting

## Feature engineering

The following transformations were applied:

- year: extraction of the 4-digit year from raw text patterns
- duration: conversion from text format to numeric minutes
- votes: numeric conversion after separator cleanup
- gross_income: custom parser to convert heterogeneous formats into numeric values
- votes_log: logarithmic transformation of votes
- gross_income_log: logarithmic transformation of gross_income
- certificate_encoded: categorical encoding
- genre_encoded: target encoding

These transformations were necessary to produce a consistent feature space for machine learning.

## Modeling approach
1. Gaussian Naive Bayes

This is the main model required by the academic statement.
It provides a simple probabilistic baseline for multiclass classification on continuous variables.

2. Random Forest

Random Forest was introduced as a more flexible comparison model, able to capture nonlinear relationships and interactions between features.

3. Gradient Boosting

The goal is not only to report accuracy, but also to compare:

- macro precision
- macro recall
- macro F1-score
- class-specific strengths and weaknesses
- confusion patterns between genres

## Evaluation metrics

Because this is a multiclass classification problem, several metrics are used:

- Accuracy — overall proportion of correct predictions
- Precision (macro) — average precision across classes
- Recall (macro) — average recall across classes
- F1-score (macro) — balanced measure between precision and recall

Macro metrics are especially important here because they give equal weight to each genre, regardless of class frequency.

## Key methodological choices

Several decisions were made to improve the rigor of the project:

- only the top N  genres were kept to reduce instability caused by rare classes
- the genre field was simplified to the main genre
- noisy numerical fields were explicitly cleaned instead of blindly converted
- transformations were justified from a statistical point of view
- model comparison was used to move beyond a single baseline

## Main limitations

This project has several limitations that should be acknowledged:

- genre is reduced to a single main label, while movies may belong to multiple genres
- only structured numerical and encoded variables are used
- textual information such as plot summaries is not exploited
- gross_income contains many zero values, which limits its - predictive power
- even with proper preprocessing, predicting genre from tabular metadata remains a difficult task

As a result, the project should be interpreted as a rigorous structured-data classification study rather than a complete genre understanding system.

## Installation

Create and activate a virtual environment, then install dependencies.

```bash
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

## Running the project

Open the notebooks in VS Code or Jupyter and execute them in this order:

1- notebooks/01_preparation_donnees.ipynb
2- notebooks/02_entrainement_modeles.ipynb

The second notebook depends on the processed files generated by the first one.

## Expected outputs

After running the notebooks, the project should produce:

- a cleaned processed dataset
- a label mapping file
- evaluation tables
- confusion matrices
- comparative metrics across models
- optional saved models and reports

## 👤 Author
Kenzi Mohamed Lali

Mohamed Mehdi Kharrat