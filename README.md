# QUALIFY
### Qualify: Sleep Quality Prediction using Supervised Machine Learning

Course: CS316 – Introduction to AI and Data Science
Instructor: Dr. Heyfa Ammar
Term: 261

A machine learning project focused on predicting sleep quality based on lifestyle and health-related features.

## Overview

Qualify is a machine-learning project that explores how lifestyle and health-related factors are associated with sleep quality. It develops models for two related tasks:
1. Regression: predict a numerical quality_of_sleep score.
2. Classification: categorize sleep quality as low, medium, or high, according to numerical sleep score ranges
3. 

The project workflow involves:
- Data cleaning
- Exploratory Data Analysis (EDA)
- Preprocessing pipelines
- Feature engineering
- Model training and cross-validation
- Hyperparameter tuning
- Held-out test evaluation
- Considering the responsible use and limitations of predictions about personal well-being.

## Project objectives

- Clean and prepare sleep-health data for analysis.
- Explore relationships between sleep quality and lifestyle features using summary statistics and visualizations.
- Build reproducible preprocessing pipelines for numerical and categorical variables.
- Compare original features with engineered features.
- Train and evaluate regression and classification models using appropriate metrics.
- Select models based on validation and test performance, while checking for overfitting.
- Discuss the practical value and limitations of using lifestyle data to estimate sleep quality.
  
## Dataset
The notebook reads the following CSV file from the project’s raw-data folder:
```text
data/
└── raw/
    └── Sleep_health_and_lifestyle_dataset.csv
```

Place the dataset at that exact path before running the notebook. If the dataset is not included in this GitHub repository, obtain it from the source used by your team and make sure you have permission to redistribute it.

The notebook standardizes column names and categorical text, normalizes BMI category labels, removes the person identifier and duplicate rows, drops records without a target value, and filters records that fail the notebook's validity rules. The rules remove records with age below 18, heart rate above 120, or sleep duration above 12 hours.

The main target is quality_of_sleep. The classification target, sleep_quality_class, is derived from that score using these categories:

### Sleep Quality Classes

| Class | Rule |
|------|------|
| Low | Score below 6 |
| Medium | Score from 6 up to (but not including) 8 |
| High | Score of 8 or above |


## Input features

The notebook uses eight original input features:
- Numerical: age, daily_steps, heart_rate, physical_activity_level, sleep_duration, stress_level
- Categorical: gender, bmi_category

The notebook also experiments with four engineered features:
- Stress–sleep interaction
- Stress–heart-rate interaction
- Steps per activity level
- Absolute deviation of sleep duration from 8 hours
## Methods

### Data Analysis and Preprocessing
The notebook includes:

- Dataset inspection and summary statistics
- Class-distribution plots, feature distributions, and correlation analysis
- A stratified 80/20 train-test split using random state 42
- Numerical missing-value imputation using the median and feature scaling with `StandardScaler`
- Categorical missing-value imputation using the most frequent value and one-hot encoding
- Feature engineering and comparison between original and engineered features

Preprocessing is organized into scikit-learn pipelines so transformations can be fitted on training data and applied consistently to held-out data.

### Models
The notebook compares baseline and machine-learning models for both tasks.

#### Regression
- Mean baseline (`DummyRegressor`)
- Linear Regression
- Ridge Regression with hyperparameter tuning
- Random Forest Regressor with hyperparameter tuning

#### Classification
- Majority-class baseline (`DummyClassifier`)
- Logistic Regression
- Tuned Logistic Regression
- Random Forest Classifier with hyperparameter tuning

Cross-validation is used during model comparison and tuning. The notebook evaluates regression using metrics such as R², MAE, and RMSE, and classification using accuracy, macro F1, and a confusion matrix. Random Forest models are also examined for possible overfitting and feature importance.

---

## Main Findings

According to the final model-selection discussion in the notebook:

- Regression: Linear Regression was selected to predict the numerical sleep-quality score. The notebook reports a held-out test R² of 0.951 and RMSE of 0.293 for this model.
- Classification: The tuned Random Forest Classifier was selected to predict low, medium, and high sleep-quality categories. The notebook reports a held-out test accuracy of 0.963 and macro F1 of 0.877 for this model.
- Feature analysis highlights stress level and sleep duration as important variables associated with sleep-quality scores.
- Engineered interactions are also evaluated to determine whether they improve model performance.

These are the results reported by the current notebook; rerunning the notebook may produce different results if the dataset, environment, or code changes.

---

## Repository Structure

The notebook expects the following project paths relative to its working directory. Create the folders as needed; the notebook creates the processed-data, figures, and results output folders.

```text
project-root/
├── notebooks/
│   └── QUALIFY_final (1).ipynb
├── data/
│   ├── raw/
│   │   └── Sleep_health_and_lifestyle_dataset.csv
│   └── processed/
├── figures/
├── results/
├── README.md

```
If you keep the notebook in the repository root instead of notebooks/, adjust the paths in the notebook or run it from a directory where ../data/raw resolves correctly. The current notebook defines its paths as ../data/raw, ../data/processed, ../figures, and ../results.

## Requirements

Use Python 3.10 or a compatible Python version with the following packages:

- numpy
- pandas
- matplotlib
- seaborn
- scikit-learn
- joblib
- jupyter (to run the notebook locally)
  
Install the packages with:
pip install numpy pandas matplotlib seaborn scikit-learn joblib jupyter

## How to run
1. Clone or download this repository.
2. Put Sleep_health_and_lifestyle_dataset.csv in data/raw/.
3. Install the required Python packages.
4. Open the notebook in Jupyter Notebook, JupyterLab, or Google Colab.
5. Make sure the notebook's working directory and relative paths match the repository structure.
6. Run the notebook cells from top to bottom. The notebook performs cleaning, analysis, training, evaluation, and saves result files under the configured output folders.
   
If you use Google Colab, upload the notebook and dataset or mount the storage location containing them, then update the paths if necessary.

## Responsible use, ethics, and sustainability

Sleep-quality predictions can help explore patterns in sleep and lifestyle data, but they should not be treated as a medical diagnosis or a substitute for advice from a qualified healthcare professional.

Responsible use considerations include:

- Privacy: avoid publishing identifiable or sensitive individual-level data.
- Fairness: assess whether performance differs across relevant groups, where the dataset supports such analysis.
- Transparency: document data cleaning, feature construction, model selection, and evaluation.
- Limitations: dataset quality, sample size, self-reported or subjective measures, and patterns in the source data may affect generalizability. Correlation does not establish causation.
- Sustainability and social impact: better understanding of sleep and lifestyle patterns may support well-being, which relates to UN Sustainable Development Goal 3: Good Health and Well-Being. This project is exploratory and does not establish that using the models directly improves health outcomes.
  
## Limitations and future work

Potential next steps include:

- Evaluate the selected models on an independent external dataset.
- Report class-wise precision, recall, and F1, and investigate errors across groups.
- Assess calibration and robustness to missing or out-of-range inputs.
- Compare additional algorithms and explainability methods.
- Improve documentation of dataset provenance, licensing, and reproducibility.
  
## Course context
This project was developed for CS316: Introduction to AI and Data Science in Term 261. The course project emphasizes applying AI and data science techniques to a meaningful problem while considering sustainability, ethical issues, and societal impact.

## AI-use statement
Complete this section to accurately reflect your team's process before submission:
AI tools used: [Name the tools, if any.]
How they were used: [Describe whether AI assisted with brainstorming, explanations, code, debugging, writing, or editing.]
Human verification: [Explain how the team reviewed, tested, and verified any AI-assisted material.]


