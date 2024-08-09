



# README: VAR Estimation of Stablecoin Circulation Based on Macro-Finance Variables

## Introduction

This document outlines the methodology for estimating stablecoin circulation using a Vector Autoregression (VAR) model. The estimation relies on macro-finance variables, including central bank reserve balances, S&P 500 returns, yield changes, and BTC returns. The objective is to forecast stablecoin circulation over a 6-month horizon using monthly data.

## 1. Motivation for Using a VAR Model

### Capturing Interdependencies

VAR models are powerful in capturing the interdependencies between multiple time series. Macro-finance variables and stablecoin circulation are likely to influence each other, and a VAR model can effectively capture these dynamic relationships.

### Flexibility and Empirical Success

The VAR model's flexibility allows it to handle complex relationships without imposing restrictive assumptions. Moreover, VAR models have been successfully applied in numerous macroeconomic and financial forecasting scenarios, making them a reliable choice for this analysis.

### Forecasting Capability

VAR models are widely recognized for their short- to medium-term forecasting accuracy, aligning well with the 6-month horizon of this study.

## 2. Data Description

The analysis uses monthly data for the following variables:

- **Stablecoin Circulation** (`Y_t`): The total circulation of a specific stablecoin or a basket of stablecoins.
- **Central Bank Reserve Balances** (`X1_t`): The total reserves held by central banks.
- **S&P 500 Returns** (`X2_t`): Monthly returns on the S&P 500 index.
- **Yield Changes** (`X3_t`): Monthly changes in the yield of a benchmark bond (e.g., 10-year Treasury yield).
- **BTC Returns** (`X4_t`): Monthly returns on Bitcoin.

The time series should span a period that captures various economic cycles and shocks.

## 3. Methodology

### 3.1. Preprocessing

1. **Stationarity Check**: 
   - Use the Augmented Dickey-Fuller (ADF) test to check for stationarity. If any series is non-stationary, difference it until stationarity is achieved.
   
   \[
   \Delta X_t = X_t - X_{t-1}
   \]

2. **Lag Length Selection**:
   - Determine the appropriate lag length using criteria such as the Akaike Information Criterion (AIC). To avoid overfitting, we conservatively bias toward simplicity with fewer lags.

### 3.2. Model Specification

The VAR model is specified as:

\[
\mathbf{Y}_t = \mathbf{A}_1 \mathbf{Y}_{t-1} + \mathbf{A}_2 \mathbf{Y}_{t-2} + \dots + \mathbf{A}_p \mathbf{Y}_{t-p} + \mathbf{u}_t
\]

Where:

- \( \mathbf{Y}_t = \begin{pmatrix} Y_t \\ X1_t \\ X2_t \\ X3_t \\ X4_t \end{pmatrix} \) is the vector of endogenous variables.
- \( \mathbf{A}_i \) are matrices of coefficients for the \( i \)-th lag.
- \( p \) is the number of lags included.
- \( \mathbf{u}_t \) is a vector of error terms assumed to be white noise.

### 3.3. Estimation

- Estimate the VAR model using Ordinary Least Squares (OLS) for each equation in the system.
- Ensure consistency across the model by including the same lagged variables as predictors in each equation.

### 3.4. Model Validation

**Stability Check**: 
- Check the eigenvalues of the characteristic polynomial to ensure they lie within the unit circle. This confirms the stability of the VAR system and ensures that the forecasts will converge.

**Autocorrelation Check**: 
- Use the Ljung-Box test to detect any autocorrelation in the residuals. If autocorrelation is present, consider re-specifying the model.

**Granger Causality Tests**:
- Conduct Granger causality tests to understand the directional influence between variables. This helps in validating whether the included variables significantly influence stablecoin circulation.

**Impulse Response Functions (IRFs)**:
- Generate IRFs to analyze the response of stablecoin circulation to shocks in each of the macro-finance variables. IRFs offer insight into the dynamic effects of shocks over time.

### 3.5. Forecasting

- Use the validated VAR model to forecast stablecoin circulation \( Y_{t+h} \) for \( h = 1, 2, \dots, 6 \) months ahead.
- Calculate forecast intervals to assess the uncertainty associated with the forecasts.
