# GDP Growth Forecasting with LSTM

This project implements a machine learning pipeline to forecast U.S. GDP growth using macroeconomic and financial indicators. The model leverages **Long Short-Term Memory (LSTM)** networks and historical data from the **Federal Reserve Economic Data (FRED)** database.

---

## Table of Contents

- [Project Overview](#project-overview)  
- [Data](#data)  
- [Model](#model)  
- [Results](#results)   

---

## Project Overview

Forecasting macroeconomic variables such as GDP growth is crucial for financial and policy decision-making. This project demonstrates how to:

- Collect and preprocess macroeconomic and financial data from FRED.
- Engineer features such as GDP growth rates and yield curves.
- Scale data and create sequences suitable for LSTM networks.
- Train and evaluate an LSTM model for predicting next-quarter GDP growth.

---

## Data

The data is sourced from [FRED](https://fred.stlouisfed.org/) via the `fredapi` Python library. Key series include:

| Variable        | FRED Code   | Description                             |
|-----------------|------------|-----------------------------------------|
| GDP             | GDPC1      | Real Gross Domestic Product             |
| Unemployment    | UNRATE     | Unemployment Rate                        |
| CPI             | CPIAUCSL   | Consumer Price Index                     |
| Fed Funds Rate  | FEDFUNDS   | Effective Federal Funds Rate             |
| 10-Year Yield   | GS10       | 10-Year Treasury Constant Maturity Rate  |
| 3-Month Yield   | TB3MS      | 3-Month Treasury Bill Rate               |

Derived features:

- `gdp_growth` → quarterly log difference of GDP  
- `yield_curve` → 10-year minus 3-month treasury yield  

All processed data is saved as `cleaned_data.csv`.

---

## Model

Architecture: Single LSTM layer (32 units) + Dense output
Loss Function: Huber Loss
Optimizer: Adam (learning rate = 0.001)
Input: Sequences of length WINDOW_SIZE = 2 quarters
Output: Next-quarter GDP growth

---

## Results

The LSTM model captures general trends in GDP growth but does not perfectly match all fluctuations in the test period. Deviations are especially noticeable during volatile economic periods.