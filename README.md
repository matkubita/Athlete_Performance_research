# Running Performance & Efficiency Analysis

**Authors:** Jan Zubalewicz & Mateusz Kubita

## 🎯 Project Objective
The primary goal of this project is to build a reliable model to predict a runner's **efficiency_score** based on physiological and biomechanical data. By analyzing metrics like $VO_2$ max, heart rate variability, and running mechanics, we aim to discover which machine learning algorithms best capture the complexity of endurance running performance.

## 📊 Dataset Overview
The dataset focuses on 1,158 endurance runners, capturing:
* **Demographics:** Age, Gender (Encoded: Female=1, Male=0).
* **Physiological Data:** $VO_2$ max, HRV, Lactate Threshold, Resting and Max Heart Rate.
* **Biomechanical Data:** Stride length and Cadence.
* **Target Variable:** `efficiency_score` (A composite metric representing running economy and performance).

> **Data Cleaning:** Columns such as `athlete_id`, `sport`, and incomplete metrics like `power_output` were removed to focus the model strictly on running-related predictors.

## 🛠️ Tech Stack
* **Language:** Python
* **Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`
* **Machine Learning:** `scikit-learn` (Linear Regression, Decision Tree, Random Forest, Gradient Boosting)

## 🚀 Model Comparison & Results
We used **GridSearchCV** to optimize a Gradient Boosting Regressor, specifically to fix the severe overfitting observed in the initial Decision Tree model.

| Model | Test MSE | Training MSE | Test R² | Status |
| :--- | :--- | :--- | :--- | :--- |
| **Optimized GBR** | **218.85** | **199.74** | **-0.02** | **Best Generalization** |
| **Linear Regression** | 219.63 | 211.35 | -0.02 | Stable Baseline |
| **Random Forest** | 235.63 | 31.16 | -0.10 | Overfitting |
| **Decision Tree** | 409.68 | 0.00 | -0.91 | Severe Overfitting |



## 🔍 Key Insights
1. **Handling Overfitting:** The original Decision Tree had a 0.00 Training MSE, meaning it memorized the data. By tuning `max_depth` and `learning_rate` in the Gradient Boosting model, we created a version that generalizes much better to new runners.
2. **Predictive Drivers:** Physiological markers—specifically $VO_2$ max and Lactate Threshold—showed the highest importance in determining the `efficiency_score`.
3. **Model Complexity:** While complex models (RF/GBR) are powerful, the relatively high MSE across all models suggests that running efficiency is influenced by factors not fully captured in the current dataset (e.g., training history or elevation data).

## 📂 Project Structure
* `Athlete_Performance_Regression_Analysis_Zubalewicz_Kubita.ipynb` - Full data analysis and modeling.
* `README.md` - Project documentation.