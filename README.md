# Non-Linear Regression Model for Return Prediction: SMH ETF

This repository contains the final data engineering and predictive modeling project for the semiconductor sector. The main goal is to estimate the 3-month future return of the **VanEck Semiconductor ETF (SMH)**.

### 🏛️ Institutional Context
* **Institution:** IFTS 18 (Higher Technical Degree in Data Science and Artificial Intelligence)
* **Course:** AI Systems Modeling
* **Author:** vivarafa13

---

## 📂 Repository Structure

This project is self-contained and follows data science best practices for reproducibility:

* **`data/`**: Contains the consolidated monthly historical data matrix (`Master_Model.csv`).
* **`notebooks/`**: Contains the development environment and the Python pipeline (`RegresionNoLineal.ipynb`).
* **`.gitignore`**: Specifically configured for cloud development environments (Google Colab and AWS SageMaker Studio Lab) to isolate temporary files and virtual environments.

---

## 📈 1. Business & Functional Dimension (For Clients)

### The Problem
The semiconductor sector is the heart of modern technology and Artificial Intelligence. However, this market is highly volatile and depends heavily on macroeconomic cycles and Federal Reserve (FED) monetary policies. 

### The Goal
The objective is to build a system to **predict the medium-term return trend (3 months)** of the semiconductor industry. The model does not try to guess tomorrow's exact price. Instead, it estimates the future rate of return based on current financial and macroeconomic conditions.

The target variable (Target) is mathematically defined as:
$$Return\_3m = \frac{Price_{t+3} - Price_t}{Price_t}$$

---

## 🛠️ 2. Technical & Data Engineering Dimension (For Professors)

The pipeline implemented in the Python notebook covers the complete workflow of a professional data project:

### Data Ingestion and ETL from Different Sources
We synchronized monthly data using the last business day of each period, combining financial and real macroeconomic variables:
1. **SMH (Closing Prices):** Main indicator of the semiconductor tech sector.
2. **NASDAQ:** Proxy for the general tech stock market behavior.
3. **VIXCLS:** Implied volatility index (the market's "fear index").
4. **FEDFUNDS:** Effective Federal Funds Rate from the Federal Reserve.
5. **CPIAUCSL:** Consumer Price Index (US Inflation metric).

### Data Cleaning and Preventing Data Leakage
* **Fixing Missing Data:** We identified a missing data point in the official FRED CPI series for October 2025 (caused by an original source glitch). We resolved this by applying a **technical linear interpolation** between the previous and next months to complete the series without bias.
* **Preventing Data Leakage:** We filtered the current month and future periods using mathematical logic in Google Sheets and Python. This stopped the algorithm from training with wrong $-100\%$ labels caused by empty cells, protecting the model's accuracy.
* **Data Type Conversion:** We converted percentage strings (`%`) into real float numbers during runtime so Scikit-Learn can process the matrix correctly.

---

## 🚀 How to Run and Reproduce
The code notebook is ready to import the data matrix automatically from the repository:
1. Open `notebooks/RegresionNoLineal.ipynb`.
2. Click the **"Open in Colab"** button at the top to run the pipeline interactively in the cloud.
