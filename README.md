# Linear Model – Life Expectancy  
Multivariate Regression & Model Selection (R)

---

## Project Overview

This project analyzes determinants of global life expectancy using multivariate linear regression.

The analysis is based on the WHO Life Expectancy dataset and focuses on:

- Variable selection
- Collinearity diagnostics
- Model validation
- Outlier detection
- Predictive performance
- LASSO regularization

---

## Dataset

Source: WHO Life Expectancy Dataset  
(Kaggle: https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who)

Only year 2015 was used to avoid temporal dependency.

Outcome variable:
- LifeExp (Life expectancy)

Predictors include:
- Adult mortality
- Infant deaths
- Under-five deaths
- HIV/AIDS
- Hepatitis B
- Income
- Thinness indicators
- Vaccination coverage
- Socioeconomic indicators

---

## Initial Full Model

Full multivariate model:

LifeExp ~ all predictors (excluding Year and Country)

Key results:

- R² ≈ 0.89
- Strong predictors:
  - Income (positive effect)
  - Adult mortality (negative effect)
  - HIV/AIDS (negative effect)
  - Hepatitis B (positive effect)

---

## Variable Selection

Backward stepwise selection using AIC:

- Reduced model retained 7 predictors
- Similar explanatory power
- Improved parsimony

Collinearity diagnostics (VIF):
- Initial model showed high collinearity (e.g., infant deaths vs under-five deaths)
- Reduced model achieved VIF < 3

---

## Model Validation

Diagnostics performed:

- Residual vs fitted plots
- Q-Q plots (normality)
- Scale-location plot
- Cook’s distance
- Hat values
- Studentized residuals

Influential observations identified:
- India (high leverage)
- Zimbabwe (significant outlier)

Observations were not removed as they represent real-world data.

---

## Non-Linear Effects

Quadratic term added for thinness:

LifeExp ~ thinness + thinness² + ...

Results:
- R² improved to ≈ 0.90
- Quadratic term statistically significant
- Improved residual standard error

---

## LASSO Regression

Regularized regression using `glmnet`:

- Cross-validated LASSO
- Selected predictors at lambda.min:
  - Adult.Mortality
  - Hepatitis.B
  - Polio
  - HIV.AIDS
  - thinness
  - Income

Refit OLS on selected variables achieved:

- R² ≈ 0.89
- Similar predictive performance
- More stable coefficient structure

---

## Predictive Performance

Training (2015):
- RMSE ≈ 2.34

Testing (2014):
- RMSE ≈ 2.97

Model generalizes reasonably well.
Test RMSE remains below the standard deviation of life expectancy.

---

## Additional Analysis

- Marginal effects using `emmeans`
- Confidence intervals for coefficients
- Comparison of confidence vs prediction intervals
- Categorical analysis: Developed vs Developing countries

Developing countries showed ≈10 years lower life expectancy on average.

---

## Technologies Used

- R
- dplyr
- ggplot2
- car
- emmeans
- effects
- glmnet

---

## Skills Demonstrated

- Multivariate linear modeling
- Variable selection (AIC)
- Collinearity diagnostics (VIF)
- Influence & outlier analysis
- Polynomial modeling
- Regularization (LASSO)
- Train/Test evaluation
- Interpretation of regression coefficients
- Predictive performance assessment

---

## Note

This project focuses on statistical methodology and interpretation rather than production deployment.
