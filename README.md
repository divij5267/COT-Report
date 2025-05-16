```markdown
# Forecasting Commodity Futures Returns Using COT Data

A robust, data-driven framework for predicting short-term returns in Gold, Crude Oil, and Corn futures using CFTC Commitment of Traders (CoT) reports and continuous futures price series.

---

## Overview

This project explores whether weekly CoT data can forecast returns in major commodity futures markets. We combine rigorous feature engineering with rolling-window statistical and machine learning models, benchmarking predictive performance and feature importance across asset classes.

---

## Key Features

- **Comprehensive Data Integration**: Merges CFTC CoT positioning data with LSEG DataStream continuous futures prices (CS04) for Gold, Crude Oil, and Corn.
- **Advanced Feature Engineering**: Constructs and selects predictive features based on academic literature and industry best practices.
- **Rolling Window Modeling**: Implements linear regression, ARIMA(+GARCH), and XGBoost models using rolling training windows for robust out-of-sample evaluation.
- **Asset-Specific Analysis**: Benchmarks predictive power and model performance for each commodity, with insights into regime shifts and market structure.
- **Interpretability**: Uses Lasso and SHAP to identify and explain the most influential predictors.
- **Full Reproducibility**: All code, data, and methodology are provided for transparent, end-to-end analysis.

---

## Dataset

- **Gold (COMEX, 100 oz)**: 1995–2025
- **Crude Oil (NYMEX WTI, 1,000 barrels)**: 1995–2025
- **Corn (CBOT, 5,000 bushels)**: 2006–2025

**Data Sources:**
- **CoT Reports**: CFTC, weekly, cleaned and aligned to futures price dates.
- **Futures Prices**: LSEG DataStream CS04 (continuous, price-adjusted, expiration-rolled).

**Repository Files:**
- `Data.xlsx`: Cleaned and merged data for all three commodities.
- `Code.ipynb`: Jupyter notebook with all data processing, feature engineering, modeling, and evaluation code.
- `Explanation.pptx`: Presentation with project rationale, methodology, and results.

---

## Methodology

### Data Preprocessing

- Align CoT and CS04 data on weekly dates.
- Fill missing CS04 values with previous available price to avoid lookahead bias.
- Normalize features (e.g., ratios to open interest) for comparability across time.

### Feature Engineering

- **Base Features**: Open Interest, Noncommercial/Commercial Long/Short/Spread, CS04 price.
- **Constructed Features**:
  - Net Position, Net Change, Net Ratio, Long/Short Ratios, Z-score of Net Position, Extreme Sentiment Flags, Open Interest Change/Volatility, Interaction Terms (e.g., Long_Ratio × Short_Ratio).
- **Feature Selection**:
  - Remove low-variance and highly correlated features.
  - Lasso regression for further selection of predictive variables.

### Modeling Approach

- **Rolling Forecasts**:
  - Training window: 52 weeks for linear/XGBoost, 80 weeks for ARIMA.
  - Forecast horizon: 1 week ahead log return.
- **Models Benchmarked**:
  - Linear Regression (with/without Lasso selection)
  - XGBoost
  - ARIMA and ARIMA+GARCH
- **Evaluation Metrics**:
  - Out-of-sample (OOS) R² and Mean Squared Error (MSE)
  - Feature importance via Lasso coefficients and SHAP values

---

## Results

| Commodity   | Best Model         | OOS R² | OOS MSE | Key Insights |
|-------------|--------------------|--------|---------|--------------|
| Gold        | Linear (Lasso)     | 0.08   | 0.0057  | CoT predictive power increased post-2019 but remains modest. CS04 is less sensitive to sentiment than front-month futures. |
| Crude Oil   | Linear (Lasso)     | 0.16   | 0.0401  | Net speculative flows and OI changes are predictive. Commercial hedging is a contrarian signal. Regime shifts post-2022 require adaptive models. |
| Corn        | ARIMA(1,0,1)       | 0.28   | 0.0106  | Predictive power is seasonal and regime-dependent. Extreme positioning and OI features are most relevant. |

**General Findings:**
- CoT data is a useful, but not dominant, predictor of returns-its power varies by asset and market regime.
- Feature importance shifts over time, with net speculative flows and open interest changes consistently ranking high.

---

## Roadmap

**Phase 1: Broaden Asset Universe**
- Add more commodities (e.g., Wheat, Soybeans), financial futures, and cross-asset features.

**Phase 2: Advanced Modeling**
- Experiment with nonlinear/time-varying models (e.g., regime-switching, transformers).
- Integrate macroeconomic and alternative data (e.g., news sentiment).

**Phase 3: Real-Time and Strategy Integration**
- Use higher-frequency data for intraday prediction.
- Backtest trading strategies using front-month futures for realistic simulation.

**Phase 4: Risk Management and Explainability**
- Implement advanced risk metrics (e.g., CVaR).
- Enhance model interpretability with more granular SHAP and partial dependence plots.

---

## Installation

Clone the repository and install dependencies:

```
git clone https://github.com/yourusername/commodity-cot-forecast.git
cd commodity-cot-forecast
```

---

## Usage

1. **Open `Code.ipynb`** in Jupyter or VSCode.
2. **Ensure `Data.xlsx` is in the same directory.**
3. **Run the notebook cells** to reproduce all data processing, feature engineering, modeling, and result visualization.
4. **Refer to `Explanation.pptx`** for a summary of rationale, methodology, and key findings.

---

## Contributing

Contributions and suggestions are welcome! Please open an issue or submit a pull request.

This project was made under the guidance of Tony Gao and Mike Aguilar as a requirment for our capstone (end term project.) 

---


## Contributing

Contributions and suggestions are welcome! Please [open an issue](https://github.com/divij5267/cot-signal-lab/issues) or [submit a pull request](https://github.com/divij5267/cot-signal-lab/pulls).

This project was made under the guidance of [Tony Gao](https://www.linkedin.com/in/tonygaozitong/) and [Mike Aguilar](https://www.linkedin.com/in/mike-aguilar-econ/) as a requirement for our capstone (end term project).

## License

This project is licensed under the MIT License. See `LICENSE.md` for details.

---

## Acknowledgments

- CFTC for Commitment of Traders data
- LSEG DataStream for continuous futures prices
- Academic literature and industry reports referenced in `Explanation.pptx`

---

## Contact

- Divij Yanduru: divijyanduru1@gmail.com
- LinkedIn: www.linkedin.com/in/divijyanduru
- GitHub: https://github.com/divij5267

---
```
