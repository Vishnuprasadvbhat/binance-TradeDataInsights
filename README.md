# **📊 Binance Trade Analysis & Ranking System**  

## **🔍 Problem Statement**  
The goal of this project is to analyze **90 days of historical trade data** from multiple **Binance accounts** to evaluate their performance. The objective is to compute **key financial metrics**, rank the accounts based on performance, and identify the **top 20 most profitable traders**.  

This analysis will offer valuable insights into trading strategies, risk management, and overall profitability.  

---  

## **📂 Dataset Overview**  
The dataset includes the following key components:  

- **🆔 Port_IDs**: Unique identifiers for individual trading accounts.  
- **📜 Trade_History**: Comprehensive trade records, including:  
  - **Timestamp** ⏳: Date & time of the trade  
  - **Trading Pair** 💱: The asset being traded  
  - **Side (BUY/SELL)** 📈📉: Transaction type  
  - **Price & Quantity** 💰: Trade value and amount  
  - **Profit/Loss** 📊: Realized profit or loss  

---  

## **🎯 Project Objectives**  

### **1️⃣ Dataset Analysis & Cleaning**  
✅ Load and inspect trade data  
✅ Handle missing values & inconsistencies  

### **2️⃣ Financial Metric Calculation**  
We will compute the following key metrics for each account:  

- **📊 ROI (Return on Investment)** – Measures profitability percentage.  
- **💰 PnL (Profit & Loss)** – Net earnings or losses.  
- **📈 Sharpe Ratio** – Risk-adjusted return indicator.  
- **📉 MDD (Maximum Drawdown)** – Measures worst-case loss.  
- **🏆 Win Rate** – Percentage of profitable trades.  
- **🔹 Win Positions** – Number of winning trades.  
- **🔢 Total Positions** – Total trades executed.  

### **3️⃣ Feature Engineering & Ranking Algorithm**  
✔ Determine **feature importance** using ML models.  
✔ Assign **weighted scores** based on importance.  
✔ Develop a **ranking algorithm** to sort accounts.  

### **4️⃣ Reporting & Insights**  
📌 Provide a **concise report** on findings, methodology & assumptions.  

---  

## **📦 Project Deliverables**  

✔ **🔢 Jupyter Notebook / Python Script** – Complete code & analysis.  
✔ **📄 CSV File** – Dataset with calculated financial metrics.  
✔ **🏆 Top 20 Accounts List** – Ranked based on performance.  
✔ **📜 Report** – Summary of findings & key insights.  

---  

## **📌 Additional Notes**  
📌 **Win Positions** = Number of profitable trades.  
📌 **Position Classification**:  
   - Combine **side** & **positionSide** to label trades (**e.g., long_open, long_close**).  
📌 **Money vs. Coin Quantity**:  
   - **quantity** = Amount in USD  
   - **qty** = Amount in coins  
📌 **realizedProfit** = Direct indicator of PnL (profit/loss).  

---

## **🚀 Steps to Proceed**
### **1️⃣ Data Preprocessing**
#### **1.1 Import Libraries & Read Data**
- Load essential libraries such as `pandas`, `numpy`, `matplotlib`, and `seaborn`.
- Read the dataset into a pandas DataFrame.

#### **1.2 Sanity Check of the Dataset**
- Inspect the dataset for inconsistencies and missing values.
- Ensure that all necessary columns are present and correctly formatted.

#### **1.3 Exploratory Data Analysis (EDA)**
- Perform an initial analysis to understand the dataset.
- Visualize data distributions and relationships between variables.

#### **1.4 Outlier Treatment (if Needed)**
- Detect and handle outliers using methods such as trimming, capping, or transformations.

#### **1.5 Normalization**
- Apply normalization techniques like Min-Max Scaling or Standardization for better comparability.

#### **1.6 Encoding & Other Preprocessing Steps**
- Convert categorical variables into numerical format if required.
- Handle any additional data preprocessing needs.

---

## **📊 Data Processing & Feature Engineering**
### **2️⃣ Handling String-Based Data**
- Initial dataset exploration revealed that the entire data was stored as a **string**.
- Using the `Abstract Syntax Tree (AST)`, we converted string data into a list and processed it.
- The dataset was then **exploded** into separate features and **joined back** for structured analysis.

### **3️⃣ Understanding Key Data Fields**
#### **Dataset Headers & Explanation:**
| Column Name        | Description |
|--------------------|-------------|
| **Port_IDs**       | Unique identifier for the portfolio. |
| **time**           | Timestamp of the transaction (Unix time). |
| **symbol**         | Trading pair (e.g., SOLUSDT, BTCUSDT). |
| **side**           | Trade direction (BUY/SELL). |
| **price**          | Price at which the asset was traded. |
| **fee**            | Transaction fee. |
| **feeAsset**       | Asset in which the fee is paid. |
| **quantity**       | Quantity of the asset traded. |
| **quantityAsset**  | Asset in which the quantity is specified. |
| **realizedProfit** | Profit or loss from the transaction. |
| **realizedProfitAsset** | Asset in which profit is measured. |
| **baseAsset**      | Base asset in the trading pair. |
| **qty**            | Quantity of the base asset traded. |
| **positionSide**   | Long/Short position indicator. |
| **activeBuy**      | Indicates if the trade was an active buy. |

---

## **🔎 Exploratory Data Analysis (EDA) Findings**
### **Key Observations:**
- **High Skewness**: Data is highly skewed with extreme values influencing price, quantity, and realized profit.
- **Outliers Identified**: Many values fall outside the **Interquartile Range (IQR)**.
- **Profit Variations**: Some traders exhibit extreme variations in profits and losses.
- **Fee Structure**: Negative fees represent rebates.
- **Trading Preferences**:
  - Users buy **high volumes of lower-priced coins**.
  - Moderate trading volumes are observed for higher-priced coins.
  
#### **Numerical Columns Identified:**
- `Port_IDs`, `price`, `fee`, `quantity`, `realizedProfit`, `qty`

#### **Categorical Columns Identified:**
- `symbol`, `side`, `feeAsset`, `quantityAsset`, `realizedProfitAsset`, `baseAsset`, `positionSide`

#### **Top 3 Traded Coins:**
1. **1000PEPE** (1000Pepe)
2. **ETH** (Ethereum)
3. **BTC** (Bitcoin)

---

## **📈 Key Financial Metrics to Calculate**
### **4️⃣ Metrics for Performance Ranking**
#### **1. ROI (Return on Investment)**
- Formula:
  
  \[ ROI = \frac{\sum \text{realized profits}}{\sum (\text{entry price} \times \text{quantity})} \]
- Includes adjustments for fees if necessary.

#### **2. Profit & Loss (PnL)**
- Measures net earnings or losses per trade.

#### **3. Sharpe Ratio (Risk-Adjusted Return)**
- Formula:
  
  \[ Sharpe Ratio = \frac{\text{Mean (PnL)}}{\text{Standard Deviation (PnL)}} \]
- Assumes a **risk-free rate of 0** in crypto trading.

#### **4. Maximum Drawdown (MDD)**
- Measures the **largest peak-to-trough** decline in portfolio value.
- Helps assess **worst-case losses**.

#### **5. Win Rate**
- Percentage of trades where **profit > 0**.

#### **6. Win Positions**
- Total number of **profitable trades**.

#### **7. Total Positions**
- Total number of **trades executed**.

---

## **🏆 Ranking Algorithm**
### **5️⃣ Feature Importance & Weighted Scoring**
- Assign **weights** to calculated metrics based on feature importance.
- Compute a final **score** for ranking accounts:
  
  \[ \text{Score} = \sum (\text{Metric Value} \times \text{Weight}) \]
- The **top 20 ranked accounts** are selected.

### **Ranking Output:**
- **model_df.nsmallest(20, 'rank')[['account_id', 'ROI', 'rank']]**
- Extracts **top accounts based on score.**

---

## **📦 Final Deliverables**
✔ **🔢 Jupyter Notebook / Python Script** – Full implementation.
✔ **📄 CSV File** – `metrics.csv` Dataset with calculated financial metrics.
✔ **🏆 Top 20 Accounts List** – Based on ranking.
✔ **📜 Report** – Summary of findings & insights.

---

## **📌 Conclusion**
This project provides a **systematic approach** to analyzing Binance trade data, applying **financial metrics**, and using **machine learning-based ranking**. The insights derived can help **identify top-performing traders** and **understand trading patterns**, making it a valuable tool for financial analysis and risk assessment.
