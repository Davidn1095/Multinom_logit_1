# Multinom_logit_1

Multinomial logistic regression analysis.

The script involves reading and preparing data, fitting a multinomial logistic regression model, examining the model's coefficients and their significance, making predictions, and evaluating the model's fit and accuracy.

### Reading Data from a CSV File:

- `Chapman.Cuali <- read.csv("Chapman_Cuali.csv", header = T, sep = ",", stringsAsFactors = T)`: Reads data from "Chapman_Cuali.csv" into a DataFrame `Chapman.Cuali`. The `header = T` indicates that the first row contains column headers. `stringsAsFactors = T` converts string columns to factors.

### Factor Releveling and Creation:

- `Chapman.Cuali$Presion <- factor(Chapman.Cuali$Presion, levels = c("Optima", "Normal", "Alta", "Descompensada"))`: Converts the `Presion` column into a factor with specified levels in a specific order.
- `Chapman.Cuali$IMC <- factor(Chapman.Cuali$IMC, levels = c("Normal", "Sobrepeso", "Obesidad"))`: Converts the `IMC` column into a factor with specified levels.

### Loading the nnet Package and Fitting Multinomial Logistic Regression:

- `library(nnet)`: Loads the `nnet` package which contains functions for fitting multinomial logistic regression models.
- `Ajuste.Multinom.Cuanti <- multinom(Presion ~ Edad + Colesterol, data = Chapman.Cuali)`: Fits a multinomial logistic regression model with `Presion` as the response variable and `Edad` and `Colesterol` as predictors.

### Model Summary and Odds Ratios:

- `summary(Ajuste.Multinom.Cuanti)`: Provides a summary of the fitted multinomial logistic regression model.
- `exp(summary(Ajuste.Multinom.Cuanti)$coefficients)`: Exponentiates the model's coefficients to interpret them as odds ratios.

### Coefficient Significance Testing:

- The next block of code calculates the z-scores for each model coefficient (coefficients divided by their standard errors) and then computes the two-tailed p-values for these z-scores.

### Confidence Intervals and Exponentiated Confidence Intervals:

- `confint(Ajuste.Multinom.Cuanti)`: Calculates the confidence intervals for the model parameters.
- `exp(confint(Ajuste.Multinom.Cuanti))`: Exponentiates the confidence intervals to interpret them as odds ratios.

### Predictions from the Model:

- `predict(Ajuste.Multinom.Cuanti, type = "probs")[1:10,]`: Predicts probabilities for the first 10 observations in the dataset.
- `predict(Ajuste.Multinom.Cuanti, type = "class")[1:10]`: Predicts the class for the first 10 observations.

### Comparing Predicted Classes with Actual Data:

- `table(Chapman.Cuali$Presion, predict(Ajuste.Multinom.Cuanti, type = "class"))`: Creates a contingency table to compare the actual `Presion` levels with those predicted by the model.

### Model Deviance and Significance Testing:

- `Ajuste.Multinom.Cuanti$deviance`: Retrieves the deviance of the fitted model.
- `pchisq(Ajuste.Multinom.Cuanti$deviance, 591, lower.tail = F)`: Calculates the p-value for the deviance statistic, which tests the overall significance of the model. Here, 591 should be the degrees of freedom, which is usually the difference between the number of observations and the number of parameters estimated.
