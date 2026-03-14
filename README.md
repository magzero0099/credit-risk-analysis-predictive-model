This project focuses on the analysis of loan default data and the development of a predictive model capable of estimating the probability that a loan will default. The work combines data cleaning, feature engineering, statistical analysis, and machine learning techniques implemented in Python. The final model is based on logistic regression and is designed to support credit risk assessment. 

## Project Overview

Banks and financial institutions rely on credit risk models to estimate whether a borrower is likely to repay a loan. In this project, a dataset containing information on 10,000 loans issued between 2008 and 2018 was analyzed in order to:

- study the main factors related to loan default,
- preprocess and transform the dataset,
- build a predictive logistic regression model,
- evaluate the model using appropriate credit-risk metrics,
- extract conclusions about the characteristics of defaulting borrowers.

The project was developed entirely in Python and combines machine learning with statistical hypothesis testing.

## Objectives

The main objectives of the project were:

1. To analyze a banking dataset and extract meaningful conclusions.
2. To build a model capable of predicting loan default risk.
3. To identify which numerical and categorical variables are most strongly related to default.
4. To evaluate whether the resulting model is suitable for credit risk applications.

## Dataset

The dataset contains information about ~10,000 loans. Each row represents a loan application, and the target variable indicates whether the loan defaulted (`1`) or not (`0`). The data includes:

### Numerical features
- `income`: applicant annual income
- `install_to_inc`: installment-to-income ratio
- `loan_amount`: loan principal
- `term_length`: loan duration in months
- `schufa`: external credit score

### Categorical features
- `occup`: employment status
- `marital`: marital status
- `num_applic`: number of applicants

### Additional variable
- `OBS_DATE`: loan application date

### Target
- `target_var`: loan default status 

## Methodology

### 1. Data Cleaning and Missing Value Handling

The original dataset contained missing values. Some records with missing values in essential fields such as application date, external score (schufa), or target variable were removed because they could not be recovered. For other numerical variables with known relationships, missing values were inferred mathematically when possible. In cases where more than one related value was missing, regression trees were used to estimate them. This allowed the project to preserve a large portion of the original data.

### 2. Train/Test Split

The dataset was split into training and test sets using an approximate 70/30 ratio. The class distribution between defaulted and non-defaulted loans was preserved in both subsets to avoid introducing additional bias during model evaluation. 

### 3. Categorical Feature Transformation

Categorical variables were analyzed and grouped when categories did not show statistically significant differences in default probability. Hypothesis testing was used to merge classes into more meaningful groups.

Examples:
- Employment status was grouped into: `Employee`, `Student`, `Unemployed`
- Marital status was grouped into: `Married`, `Living together`, `Single`, `Divorced/Separated`
- Number of applicants was simplified to: `1` or `2`  

### 4. Numerical Feature Transformation

Several numerical variables showed skewed distributions. To improve model performance and normalize the variables, different transformations were tested, including:

- logarithmic transformation,
- square root transformation,
- Box-Cox transformation.

According to the analysis, Box-Cox generally performed best, especially for highly skewed variables. (Note that the Box-Cox transformation applies both logarithmic and square root transformations for certain values of its parameter lambda)

### 5. Feature Selection

Feature selection was performed using:
- **ANOVA** for numerical variables,
- **chi-square tests** for categorical variables.

Later, recursive feature elimination with cross-validation (RFECV) was applied using logistic regression and AUROC as the scoring metric. The final conclusion was that the model performed best when keeping all selected variables. 

### 6. Model Training

The final model was a **logistic regression classifier**. Hyperparameter tuning was performed using **grid search with cross-validation** to find the best parameter combination. The model was trained on the training set and evaluated on the test set.

## Model Evaluation

Because the task is related to credit risk, the project emphasized not only classification performance but also the model’s ability to assign reliable default probabilities.

The main evaluation metrics were:

- **Gini coefficient**
- **F1 score**
- **ROC curve / AUROC**
- **Confusion matrix**

### Main results
- **Gini coefficient:** approximately **0.85**
- **F1 score:** approximately **0.60**

These results suggest that the model is strong at ranking loans by risk and assigning meaningful default probabilities, although it is less effective when making hard class predictions around uncertain cases. This makes it more suitable for credit risk scoring than for strict binary classification tasks. 

## Key Findings from the Data Analysis

The analysis revealed several relevant patterns:

- Defaulting clients tend to have **lower incomes**.
- They also show a **higher installment-to-income ratio**.
- They receive a **lower external credit score**.
- Default is more frequent among **unemployed** borrowers, followed by **students**, and less frequent among **employed** borrowers.
- In marital status, default is more frequent among **divorced/separated** and **single** applicants, and lower among **married** applicants.
- Loans requested by **one single applicant** default more often than those requested by **two applicants**.

The project also concluded that:

- The most influential numerical variable was **external score (`schufa`)**.
- The least influential numerical variable was **loan amount**.
- The most influential categorical variable was **employment status**.

## Conclusions

The project successfully achieved its two main goals:

1. Building a predictive model for loan default risk,
2. Extracting useful insights from the dataset.

Although the model is not perfect as a pure classifier, it performs very well as a **credit scoring tool**, which was the main purpose of the project. The results show that logistic regression, together with careful preprocessing and statistical analysis, can be an effective and interpretable solution for loan default prediction.

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib / Seaborn
- Scikit-learn
- SciPy
