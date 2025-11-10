# 🚲 Assignment 8 — Ensemble Learning on Bike Sharing Data  
### *A Step-by-Step End-to-End Machine Learning Pipeline with Ensemble Methods, Bias–Variance Analysis, and Hypothesis Evaluation*

---
#### Name: Aditya Thakur &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Roll No: DA25M004
---
## 📘 Project Overview

This project predicts hourly bike rental counts (`cnt`) using the **UCI Bike Sharing Dataset**.  
It demonstrates an end-to-end ML workflow with focus on **ensemble learning** methods—Bagging, Boosting, and Stacking—and evaluates their performance through **bias–variance tradeoff** and **hypothesis validation**.

---


## ✅ 1) Dataset Information

- Dataset: UCI Bike Sharing Dataset  
- File required: `hour.csv`
- Target variable: `cnt` (hourly total number of rentals)


# ✅ 2) Step-by-Step ML Pipeline

---

## 🔍 2.1 Data Loading & Inspection

Checks performed:
- Missing values → none  
- Null values → none  
- Duplicate rows → none  
- Constant columns → none  
- Negative values → none  

✅ Dataset is clean.

---

## 🧼 2.2 Data Preprocessing

Dropped irrelevant columns:
```
instant, dteday, casual, registered
```

One-Hot Encoded categorical variables:
```
season, weathersit, mnth, hr, weekday
```

Ensured dummy columns are integer (0/1).

---

## ✂️ 2.3 Train–Test Split

- train: 80%  
- test: 20%  
- random_state=42 for reproducibility

```
X = df_encoded.drop('cnt', axis=1)
y = df_encoded['cnt']
```

---

## 🧪 2.4 Baseline Models

### DecisionTreeRegressor(max_depth=6)
- Train RMSE: 119.51  
- Test RMSE: 118.46  

### Linear Regression
- Train RMSE: 101.92  
- Test RMSE: 100.45  

✅ **Baseline Selected:** Linear Regression

---

# ✅ 3) Ensemble Models

---

## 🌳 3.1 Bagging — Variance Reduction

### Hypothesis  
> Bagging reduces variance by averaging multiple weak learners.

### Results:
- Train RMSE: 113.90  
- Test RMSE: 112.34  
- Gap: -1.55  

### Evaluation:
- Reduced variance vs individual tree
- Accuracy not better than Linear Regression

---

## 🚀 3.2 Gradient Boosting — Bias Reduction

### Hypothesis  
> Boosting reduces bias by sequentially correcting residuals.

### Results:
- Train RMSE: 63.93  
- Test RMSE: 64.48  
- Gap: +0.55  

### Evaluation:
- Best generalization so far
- Strong reduction in bias

---

## 🧠 3.3 Stacking — Meta-Learning

### Hypothesis  
> Stacking improves accuracy by combining diverse models using a meta-learner.

### Base Models:
- KNN(k=5)  
- Bagging Regressor  
- Gradient Boosting  

### Meta-Learner:
- Ridge Regression

### Results:
- Train RMSE: 57.22  
- Test RMSE: 60.27  
- Gap: +3.05  

### Evaluation:
- Lowest Test RMSE overall
- Slight variance increase  
- Accurate due to model diversity

---

# ✅ 4) Bias–Variance Tradeoff Summary

| Model | Train RMSE | Test RMSE | Gap |
|--------|------------|-----------|------|
| Linear Regression | 101.92 | 100.45 | -1.47 |
| Bagging | 113.90 | 112.34 | -1.55 |
| Gradient Boosting | 63.93 | 64.48 | +0.55 |
| Stacking | 57.22 | 60.27 | +3.05 |

**Insights:**
- LR → low variance, high bias  
- Bagging → reduced variance  
- Boosting → excellent bias–variance balance  
- Stacking → lowest bias, moderate variance increase

---

# ✅ 5) Final Conclusion

### ⭐ Best Model: **Stacking Regressor**
---
<img width="720" height="484" alt="4825f7a4-5a80-4ad9-9643-d0ce2a197047" src="https://github.com/user-attachments/assets/0ec77791-3ffc-4514-b087-3f20daf7927e" />
---
### Why?
- Combines complementary models (KNN, Bagging, Boosting)  
- Meta-learner (Ridge) optimally weights them  
- Achieves best predictive performance  
- Slight increase in variance acceptable due to substantial accuracy gain  

---


