[ HOME ](README.md)
# Read 13 - Linear Regressions

- Linear regression is a basic and commonly used type of predictive analysis. 
- The overall idea of regression is to examine two things: 
  - (1) does a set of predictor variables do a good job in predicting an outcome (dependent) variable?  
  - (2) Which variables in particular are significant predictors of the outcome variable, and in what way do they–indicated by the magnitude and sign of the beta estimates–impact the outcome variable? 
- These regression estimates are used to explain the relationship between **one dependent variable and one or more independent variables**. 
```
y = c + b*x
```
 - where:
    -  y = estimated dependent variable score, 
    - c = constant, b = regression coefficient, and 
    - x = score on the independent variable.
- Three major uses for regression analysis are 
    - (1) determining the strength of predictors:
        -  Typical questions are what is the strength of relationship between dose and effect, sales and marketing spending, or age and income.
    - (2) forecasting an effect:
        - understand how much the dependent variable changes with a change in one or more independent variables.  A typical question is, “how much additional sales income do I get for each additional $1000 spent on marketing?” 
    - (3) trend forecasting:
        - Predicts trends and future values.  The regression analysis can be used to get point estimates.  A typical question is, “what will the price of gold be in 6 months?”

Types of Linear Regression
 

### Simple linear regression
- 1 dependent variable (interval or ratio):
  - 1 independent variable (interval or ratio or dichotomous)

- Multiple linear regression:
  - 1 dependent variable (interval or ratio) , 2+ independent variables (interval or ratio or dichotomous)

- Logistic regression:
  - 1 dependent variable (dichotomous), 2+ independent variable(s) (interval or ratio or dichotomous)

- Ordinal regression:
  - 1 dependent variable (ordinal), 1+ independent variable(s) (nominal or dichotomous)

- Multinomial regression:
  - 1 dependent variable (nominal), 1+ independent variable(s) (interval or ratio or dichotomous)

- Discriminant analysis:
  - 1 dependent variable (nominal), 1+ independent variable(s) (interval or ratio)

---
# Implementing linear regression in Python

- **_Scikit-learn_** is a powerful Python module for machine learning. It contains function for regression, classification, clustering, model selection and dimensionality reduction.

### Example of implementing Linear Regression in Python

[Using linear regression](https://bigdata-madesimple.com/how-to-run-linear-regression-in-python-scikit-learn/)