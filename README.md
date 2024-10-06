# Bayesian-Methods-For-Response-Time-Analysis
This repository analyzes the opening response time of an electromechanical valve, focusing on seal vintage, fluid type, and coil voltage. It uses Bayesian modeling to identify key predictors influencing valve performance, complemented by exploratory data analysis and visualization to enhance understanding of these dynamics.

## Introduction

This project analyzes the opening response time (in milliseconds) of an electromechanical valve, which controls the flow of various fluids actuated by a solenoid. The focus is on determining how different factors—specifically seal vintage, fluid type, and applied coil voltage—affect the valve's response time.

## Exploratory Data Analysis

The dataset is read from a CSV file and includes various variables related to the valve's performance. Key components of the dataset include:

- **Valve.Rev**: Indicates the revision of the valve design.
- **Fluid**: Represents different fluids as masked factors.
- **Time.Between.Actuations_hr**: Time between valve actuations in hours.
- **Age**: Age of the indicated component.
- **Voltage**: The applied DC solenoid coil voltage.
- **Seal.Type**: Types of seal materials as masked factors.
- **Response.Time_ms**: The time to open the valve in milliseconds.

A preliminary analysis reveals that the response time data is right-skewed. To address this, a log transformation is applied before fitting the Bayesian regression model. Visualization techniques, including density plots, are utilized to assess the distribution of response times and how they vary with other variables.

## Modeling

A Bayesian linear model is fitted to understand which predictors significantly affect the response time. The coefficients of interest include:

- **b[1]**: Intercept
- **b[2]**: Indicator for new valve revision
- **b[3]**: Fluid type
- **b[4]**: Time between actuations
- **b[5]**: Indicator for new plunger
- **b[6]**: Indicator for new coil
- **b[7]**: Indicator for 24 volts
- **b[8]**: Indicator for seal type A
- **b[9]**: Indicator for new seal
- **Interaction Terms**: Various interactions between predictors (e.g., fluid type and voltage).

The model uses normal likelihood with normal priors on the coefficients and inverse gamma prior for the variance. A Markov Chain Monte Carlo (MCMC) simulation is conducted to sample from the posterior distribution of the parameters.

## Diagnostics and Parameter Estimation

After fitting the model, various diagnostics are performed to assess convergence and model performance:

- **Autocorrelation Diagnostics**: Checks for correlation in the sampled MCMC chains, indicating the need for potentially adjusting the model if high autocorrelation is present.
- **Effective Sample Size**: Evaluates how many independent samples were effectively obtained from the MCMC process, providing insights into the reliability of the parameter estimates.

The means of the posterior distribution for the coefficients are calculated, giving insights into the relationship between the predictors and the response variable.

## Results

The model's performance is visually assessed through density plots that compare the observed and modeled response time distributions. This visualization aids in understanding how well the model fits the actual data.

Additionally, the probability that the response time at 30 volts is less than at 24 volts is computed using the modeled posterior distribution, which provides further insights into the effects of voltage on response time.

## Conclusion

This project successfully utilizes Bayesian analysis to explore the factors influencing the opening response time of an electromechanical valve. The findings contribute to understanding the relationship between various operational conditions and valve performance, potentially guiding future designs and operational improvements.

---
