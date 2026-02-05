# Useful AI in Irish Power System

This repository contains the end-to-end research and implementation framework for **Short-Horizon Net-Load Forecasting** and **Residual-Based Anomaly Detection** tailored for the Irish Power System.

The project addresses the challenges of high wind penetration and increasing System Non-Synchronous Penetration (SNSP) on the Irish grid by providing calibrated uncertainty in forecasts and identifying operational anomalies.

## 🏗 System Architecture

The framework is divided into two primary phases:

1. **Phase A:** Bayesian Net-Load forecasting using an MC-Dropout LSTM to provide 15-minute ahead probabilistic forecasts.
2. **Phase B:** Unsupervised Anomaly Detection using residuals (forecast errors) to identify grid regime shifts.

---

## 📂 Project Pipeline & Notebooks

To replicate the results, notebooks should be executed in the following order:

### 1. Data Cleaning & Preparation

These notebooks handle the ingestion and alignment of disparate datasets spanning 2014–2025.

* **`EirGrid Cleaning final.ipynb`**: Processes 15-minute operational data. It includes critical logic for sequential timestamp correction and net-load calculation ().
* **`Met Eirean Cleaning final.ipynb`**: Aggregates hourly meteorological data from various stations into four regional quadrants (NW, NE, SW, SE) and interpolates values to match the 15-minute grid frequency.

### 2. Bayesian Forecasting (Phase A)

* **`Forecaster_notebook.ipynb` (nb1_1)**:
* **Feature Engineering**: Implements cyclical encodings and walk-forward cross-validation.
* **Model**: Defines a Deep LSTM with Monte Carlo (MC) Dropout active during inference.
* **Uncertainty Quantification**: Generates calibrated 80% and 95% confidence intervals based on 50 stochastic forward passes per prediction.



### 3. Anomaly Detection (Phase B)

* **`Anomaly_Detection_notebook.ipynb` (nb1_2)**:
* **Residual Generation**: Calculates the delta between actual net-load and the Bayesian forecast mean.
* **Unsupervised Learning**: Implements and compares four detection methodologies:
* -Thresholding (Baseline)
* Isolation Forest
* One-Class SVM (OC-SVM)
* DeepSVDD (Deep Support Vector Data Description)


* **Evaluation**: Uses custom `AnomalySafeTimeSeriesSplit` to evaluate performance across seasonal regimes (Winter vs. Summer).



---

## 📊 Validation Strategy

The project utilizes a **Walk-Forward Growing Window** validation strategy to maintain temporal integrity, ensuring no data leakage from the future into the past.

---

## 🛠 Tech Stack

* **Deep Learning**: PyTorch, PyTorch Lightning
* **Optimization**: Optuna (Hyperparameter Tuning)
* **Data Analysis**: Pandas, NumPy, Scikit-learn
* **Anomaly Detection**: PyOD
* **Storage**: HDF5 (for high-speed windowed data access)

## 📜 License

This project is licensed under the MIT License - see the LICENSE file for details.

## ✍️ Author

**Jonathan Muwanguzi** MSc in Artificial Intelligence & Machine Learning

University of Limerick