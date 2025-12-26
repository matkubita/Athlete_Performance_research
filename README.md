# Athlete Performance Regression Analysis

**Authors:** Jan Zubalewicz & Mateusz Kubita

## 🎯 Project Objective
The main objective of this project is to build a reliable model to predict athletic performance based on training and physiological data. By comparing different machine learning techniques, we aim to discover which algorithm best handles the complexity of sports data. Ultimately, this analysis helps identify the most effective predictive approach and highlights the key variables that influence final results.

## 📊 Dataset Overview
The dataset contains synthetic but realistic data for 200 athletes, capturing:
* **Athlete Information:** Age, Gender, Height (cm), Weight (kg).
* **Training Information:** Intensity (1–10), Hours per week, Recovery days.
* **Schedule & Health:** Match count, Fatigue levels, Load balance, and ACL risk scores.
* **Target Variable:** `Performance_Score` (Composite score ranging from 50–100).

## 🛠️ Tech Stack
* **Language:** Python
* **Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`
* **Machine Learning:** `scikit-learn` (Linear Regression, Decision Tree, Random Forest, Gradient Boosting)



## 🚀 Model Comparison & Results
We evaluated four different regression models based on Mean Absolute Error (MAE) and Mean Squared Error (MSE).

| Model | Test MAE | Test MSE | Training MSE | Status |
| :--- | :--- | :--- | :--- | :--- |
| **Random Forest** | **10.95** | **194.15** | 32.96 | **Best Performer** |
| **Gradient Boosting** | 11.63 | 210.02 | 20.96 | Strong competitor |
| **Linear Regression** | 11.76 | 206.83 | 202.02 | Stable but rigid |
| **Decision Tree** | 15.05 | 335.00 | 0.00 | Severe Overfitting |



## 🔍 Key Insights
1. **Model Performance:** The **Random Forest Regressor** demonstrated the best generalization capabilities, achieving the lowest errors on unseen data.
2. **Overfitting Issues:** The Decision Tree model exhibited extreme overfitting (0.00 Training MSE), indicating it memorized the noise in the training set rather than learning the underlying patterns.
3. **Linearity:** Linear Regression showed the least discrepancy between training and testing, but its higher error suggests that the relationship between physiological features and performance is non-linear.
4. **Future Work:** Further hyperparameter tuning and feature engineering (regularization for trees) are recommended to improve the $R^2$ scores and overall accuracy.

## 📂 Project Structure
* `Athlete_Performance_Regression_Analysis_Zubalewicz_Kubita.ipynb` - Full data analysis and modeling.
* `README.md` - Project documentation.