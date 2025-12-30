# Runner-to-Skier Efficiency Analysis

**Authors:** Jan Zubalewicz & Mateusz Kubita

## 🎯 Project Objective
The goal of this project is to develop a **Cross-Sport Selection Model (CSSM)** to predict a runner's potential for cross-country skiing. By evaluating physiological and biomechanical data, we compare various machine learning algorithms to identify the best predictive approach for sport-specific efficiency.

## 📊 Dataset Overview
This dataset focuses on endurance runners (1,158 records) and their physiological profiles:
* **Demographics:** Age, Gender.
* **Physiological Data:** $VO_2$ max, HRV, Lactate Threshold, Resting and Max Heart Rate.
* **Biomechanical Data:** Stride length and Cadence.
* **Target Variable:** `efficiency_score` (Predicting potential in cross-country skiing).

> **Note:** Redundant features and incomplete data (like `power_output`) were removed during preprocessing to ensure model stability.

## 🛠️ Tech Stack
* **Language:** Python
* **Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`
* **Machine Learning:** `scikit-learn` (Linear Regression, Decision Tree, Random Forest, Gradient Boosting)

## 🚀 Model Comparison & Results
Initially, complex models showed severe overfitting. After applying **GridSearchCV** and manual regularization to the Gradient Boosting model, we achieved a more stable (though challenging) baseline.

| Model | Test MSE | Training MSE | Test R² | Status |
| :--- | :--- | :--- | :--- | :--- |
| **Linear Regression** | 219.63 | 211.35 | -0.02 | Most stable baseline |
| **Optimized GBR** | **218.85** | **199.74** | **-0.02** | **Best generalization** |
| **Random Forest** | 235.63 | 31.16 | -0.10 | Overfitting |
| **Decision Tree** | 409.68 | 0.00 | -0.91 | Severe Overfitting |



## 🔍 Key Insights
1.  **Overfitting Correction:** The original Decision Tree completely memorized the data (0.00 MSE). Through hyperparameter tuning (limiting `max_depth` and `learning_rate`), we successfully closed the gap between training and test performance.
2.  **Model Stability:** The **Optimized Gradient Boosting** model (with `learning_rate: 0.01`) provided the best balance, ensuring that the model generalizes to new athletes rather than memorizing specific rows.
3.  **Predictive Challenges:** All models achieved near-zero $R^2$ scores, suggesting that the current features have a weak linear relationship with the target. This indicates that predicting skiing efficiency likely requires more sport-specific technical data.
4.  **Feature Importance:** Physiological markers like $VO_2$ max and HRV were identified as the primary drivers, confirming their importance in endurance sport transitions.

## 📂 Project Structure
* `Athlete_Performance_Regression_Analysis_Zubalewicz_Kubita.ipynb` - Full data analysis, EDA, and hyperparameter tuning.
* `README.md` - Project documentation.