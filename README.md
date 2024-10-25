# Computational Finance Project (CS 515)

This repository contains the implementation and analysis of various financial option pricing models as part of the **Computational Finance Course (CS 515)** for Fall 2024. The project focuses on applying theoretical concepts in finance through data-driven methods using Python. It covers techniques for estimating historical volatility, implementing the Black-Scholes model, and the Binomial model for pricing European options.

## Table of Contents

- [Project Overview](#project-overview)
- [Installation](#installation)
- [Data Collection](#data-collection)
- [Components](#components)
    - [1. Historical Volatility Calculation](#1-historical-volatility-calculation)
    - [2. Black-Scholes Model](#2-black-scholes-model)
    - [3. Binomial Model](#3-binomial-model)
- [Usage](#usage)
- [Results](#results)
- [References](#references)

## Project Overview

The aim of this project is to explore different models for pricing options and estimating volatility, specifically:

1. **Data Collection**: Using [yfinance API](https://pypi.org/project/yfinance/) to fetch historical stock data for Reliance (Reliance.NS).
2. **Historical Volatility Calculation**: Implementing `Standard Deviation`, `Parkinson`, `Garman Klass` and `EWMA` to calculate historical volatility.
3. **Option Pricing Models**: Implementing the `Black-Scholes Model` and `Binomial Model` to price European options based on the collected stock data.

## Installation

To run the project, clone the repository and install the required packages using the command:

```bash
pip install -r requirements.txt
```

## Data Collection

The stock price data is fetched via the **Yahoo Finance** API using the `yfinance` Python library. The default stock symbol used is **Reliance.NS** (Reliance Industries Limited, India) for this notebook. This can be adjust by ticker as desired for other stocks.

```python
ticker = "RELIANCE.NS"
reliance_stock = yf.Ticker(ticker)
df = reliance_stock.history(interval="1d", period="1y")
```

## Components

### 1. Historical Volatility Calculation

#### Methods Used:

- **Standard Deviation**: Computes volatility based on the sample standard deviation of log returns.
- **Parkinson**: A high-low estimator that incorporates intra-day price ranges to estimate volatility.
- **Garman-Klass**: Combines both the high-low and open-close prices for a more refined estimate.
- **EWMA (Exponentially Weighted Moving Average)**: Uses a smoothing parameter to assign more weight to recent data.


### 2. Black-Scholes Model

The **Black-Scholes Model** is a continuous-time model used to price European call and put options based on stock volatility, strike price, time to expiration, and other key factors.

#### Usage:
```python
call_price, put_price = black_scholes(S=stock_price, K=2600, T=0.5, r=0.06, sigma=0.22)
```

### 3. Binomial Model

The **Binomial Model** uses a binomial tree to model potential future stock prices and evaluates the price of an option by stepping backward through the tree.

#### Usage:
```python
call_price_binomial, put_price_binomial = binomial_option_prices(S=stock_price, K=2600, T=0.5, r=0.06, sigma=0.22, steps=100)
```


## Usage

1. Clone the repository and navigate to the project directory.
2. Run the Jupyter notebook to see the models, and graphs.

## Results

The project includes visualizations comparing the different volatility estimates and resulting option prices calculated using the Black-Scholes and Binomial models.

- **Comparative Analysis**: A graph shows the option prices estimated through Black-Scholes and Binomial models across various parameters.
![Call Option Price vs time steps](call_option_price_vs_time_plot.png "Call Option Price (Continuous vs Discrete Models)")

- **Volatility Estimates**: Outputs average volatility from different estimation methods.  #to change

## References

- Black, F., & Scholes, M. (1973). "The Pricing of Options and Corporate Liabilities." *Journal of Political Economy.*
- Parkinson, M. (1980). "The Extreme Value Method for Estimating the Variance of the Rate of Return." *Journal of Business.*
- Garman, M. B., & Klass, M. J. (1980). "On the Estimation of Security Price Volatilities from Historical Data." *Journal of Business.*
