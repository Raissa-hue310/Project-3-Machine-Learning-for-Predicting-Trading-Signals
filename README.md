# 📈 Project 3 — Machine Learning for Predicting Trading Signals  
**Business Intelligence Analyst Program – Willis College**  
**Author: Raïssa Matho Mekjele**

This project applies technical indicator–based feature engineering and supervised machine learning to predict Buy, Sell, and Hold trading signals for a chosen stock. Models are trained using domain-informed targets generated from MACD and RSI behavior.

The work builds directly on the cleaned and feature-engineered dataset produced in **Project 2**.

---

## 📁 1. Dataset Overview

The dataset contains daily stock market data for one selected ticker. It includes:

- Date  
- Open, High, Low, Close prices  
- Adjusted close  
- Volume  
- Returns & log-returns  
- Moving averages  
- Volatility  
- Lag features  

In Project 3, additional technical indicators were manually engineered:

- MACD (12 EMA – 26 EMA)  
- MACD Signal Line (9 EMA of MACD)  
- RSI (14-period EMA-based)  
- Bollinger Bands (20-period SMA ± 2 SD)

All indicators were computed **manually using pandas**, without external libraries.

---

## 🔧 2. Feature Engineering (Technical Indicators)- Buy signal when MACD crosses above Signal Line  
- Sell signal when MACD crosses below Signal Line  

### **RSI (Relative Strength Index)**  
RSI calculated manually using EMA smoothing:
- RSI < 30 → Buy  
- RSI > 70 → Sell  

### **Bollinger Bands**
- Middle Band = SMA20  
- Upper Band = SMA20 + 2 × SD20  
- Lower Band = SMA20 – 2 × SD20  

These features capture market trend, momentum, and volatility.

---

## 🎯 3. Trading Signal Generation (Labels)

Following assignment rules:

| Condition | Signal |
|----------|--------|
| MACD Buy **AND** RSI Buy | **Buy (1)** |
| MACD Sell **AND** RSI Sell | **Sell (-1)** |
| Otherwise | **Hold (0)** |

These signals serve as ground-truth labels (**y**) for machine learning models.

---

## 🧹 4. Data Preparation & Splitting

- Integrated indicators into the main dataframe  
- Removed NaN created by rolling windows  
- Selected predictor features (X) and labels (y)  
- Used **chronological split** (not random):
  - 80% training  
  - 20% testing  

This preserves time-series integrity.

---

## 🤖 5. Machine Learning Models Implemented

Three supervised classifiers were trained and compared:

### **1️⃣ Logistic Regression (Multinomial)**  
- Balanced class weights  
- Max iterations: 500  

### **2️⃣ Random Forest Classifier**  
- 200 trees  
- Maximum depth: 8  
- Class weights balanced  
- Captures nonlinear interactions well  

### **3️⃣ Support Vector Machine (SVM)**  
- RBF kernel  
- Balanced class weights  
- Good for non-linear decision boundaries  

---

## 📊 6. Model Evaluation

All models were evaluated using:

- Accuracy  
- Precision (macro)  
- Recall (macro)  
- F1-score (macro)  
- Confusion matrix  
- Classification report  

Random Forest typically performed best, offering better balance across Buy, Sell, and Hold classes.

---

## 🔍 7. Hyperparameter Optimization

Two models were tuned using **GridSearchCV**:

### **Random Forest:**
- n_estimators  
- max_depth  
- min_samples_split  

### **Logistic Regression:**
- Regularization strength (C)  
- Solver method  

SVM tuning was optional due to high computational cost.

---

## 📈 8. Insights & Financial Interpretation

- Combining MACD + RSI reduces noisy signals.  
- Machine learning can help detect advantageous market moments.  
- Random Forest outperforms linear models due to non-linear market structure.  
- Despite good performance, trading decisions should incorporate:
  - Risk analysis  
  - Transaction costs  
  - Market volatility  
  - Out-of-sample validation  

---

## 📁 9. Saved Outputs

Your project produces multiple files:

- Cleaned feature dataset  
- Training/test sets  
- Model predictions  
- Confusion matrices  
- Jupyter Notebook (`.ipynb`)  
- Technical Report (`.docx` / `.pdf`)  

---

## 🧑‍💻 10. Tools & Libraries Used

- Python  
- Pandas  
- NumPy  
- Scikit-learn  
- Matplotlib / Seaborn  
- Google Colab  

---

## ✔ 11. Conclusion

This project demonstrates how domain knowledge (technical indicators) combined with machine learning can support trading strategies. By generating MACD and RSI-based signals and applying classifiers (Logistic Regression, Random Forest, SVM), meaningful insights were extracted about market behavior and trends.

The methodology forms a strong foundation for more advanced predictive modeling such as LSTMs, reinforcement learning, or multi-ticker systems.

---

## ✨ Author

**Raïssa Matho Mekjele**  
Business Intelligence Analyst Program  
Willis College (Ottawa)


### **MACD (Moving Average Convergence Divergence)**  
