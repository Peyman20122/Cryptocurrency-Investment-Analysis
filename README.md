# Cryptocurrency-Investment-Analysis

Below I have written a complete, professional, clean, and ready-to-publish **README.md** for the entire project—including calculating financial metrics, categorizing currencies, and analyzing the investment portfolio with portfolio simulation—on GitHub.
Formatted + Structured + Copyable.

---

# 📊 Crypto Risk & Return Analysis

### Risk & Return Analysis of Top 20 Cryptocurrencies Using Financial Metrics and Portfolio Modeling

This project is designed to find the best cryptocurrencies for **low-risk, medium-risk, and high-risk investments**.
To do this, the most important financial metrics such as **CAGR, Volatility, Sharpe Ratio, and Max Drawdown** are calculated and then random portfolios are simulated to examine realistic investment behavior.

---

## 🧠 What are we doing in this project?

✔ Calculate daily returns for 20 cryptocurrencies
✔ Calculate 4 standard asset valuation metrics
✔ Group currencies based on performance and risk
✔ Simulate 80,000 random portfolios
✔ Draw a risk-return graph (Efficient Frontier)
✔ Show the best options for an investment portfolio

---

## 📐 Metrics used

### **1️⃣ CAGR — Average Annual Growth Rate**

A metric that shows the real growth of a currency over the long term.
Formula:

```
CAGR = (Final Price / Initial Price)^(365 / Days) - 1
```

This formula simulates **Compound Annual Return** using power and shows what the annual return would be if the price growth continued at the same rate.

---

### **2️⃣ Volatility — Price Fluctuation**

Used to measure the inherent risk of currencies.
Formula:

```
Volatility = Std(daily_returns) * sqrt(365)
```

The standard deviation shows how far the price changes deviate from the normal.
The larger it is → the more exciting and risky the currency.

---

### **3️⃣ Sharpe Ratio — profit to risk**

The most important indicator to understand whether a currency has a **reasonable profit to risk** or not.

```
Sharpe = (CAGR - risk_free_rate) / Volatility
```

* High Sharpe → currency with defensible profit
* Low Sharpe → currency with apparent profit but high risk

---

### **4️⃣ Max Drawdown — the biggest fall**

Indicates the worst fall of a currency from peak to bottom.

```
Drawdown = (Cumulative Return - Peak) / Peak
Max Drawdown = min(Drawdown)
```

A very important metric to understand how much a currency could have reduced capital in the worst case.

---

## 🧮 code for calculating criteria

```python
def calculate_metrics(x): 
x = x.dropna(subset=['daily_return']) 
days = (x['date'].iloc[-1] - x['date'].iloc[0]).days 

cagr = (x['close'].iloc[-1] / x['close'].iloc[0]) ** (365/days) - 1 
volatility = x['daily_return'].std() * np.sqrt(365) 

sharpe = (cagr - RISK_FREE_RATE) / volatility if volatility != 0 else np.nan 

cum_returns = (1 + x['daily_return']).cumprod() 
peak = cum_returns.cummax() 
drawdown = (cum_returns - peak) / peak 
max_drawdown = drawdown.min() 

return pd.Series({ 
'CAGR': cagr,
'Volatility': volatility,
'Sharpe': sharpe,
'Max_Drawdown': max_drawdown,
})
```

---

## 📊 Portfolio simulation with 80,000 random combinations

To examine the real behavior of investment portfolios, 80,000 portfolios with random weights are constructed.

```python
def make_portfo_close(df_close, df_open): 
close = df_close.to_numpy() 
open_ = df_open.to_numpy() 
R = close / open_ - 1 

Mu = R.mean(axis=0).reshape(-1, 1) 
Co = np.cov(R.T) 

nPortfolio = 80000 
Ms = np.zeros(nPortfolio) 
Ss = np.zeros(nPortfolio) 

nTicker = len(high_return_low_risk) 

for i in range(nPortfolio): 
W = GetRandomWeight(nTicker) 
Ms[i] = M(W, Mu) 
Ss[i] = S(W, Co) 

plt.scatter(Ss, Ms, s=10, c='teal') 

for i, t in enumerate(high_return_low_risk): 
W = np.zeros((nTicker, 1))
W[i, 0] = 1
m = M(W, Mu)[0]
s = S(W, Co)[0,0]
plt.scatter(s, m, s=40, c='crimson', marker='x')
plt.text(s, m, t, fontdict={'size':14})

plt.title('Return–Risk Plot for Low-Risk Portfolios')
plt.xlabel('Risk')
plt.ylabel('Return')
plt.grid()
plt.show()
```

This chart helps us understand:

* Which are the best currencies
* Where are the low-risk spots
* Which currencies only generate risk without proper returns

---

## 🧩 Final output

The project ultimately places currencies into 3 categories:

### **Low-Risk + Low volatility + Good returns**

Best options for long-term portfolio

### **Medium risk**

Suitable for diversification or medium-term investment

### **High risk**

High returns but sharp drops and high volatility

---

## 🚀 Conclusion

By combining standard financial metrics + portfolio analysis + historical behavior analysis, it is possible to choose currencies that have both **appropriate returns** and **manageable risks**.

This project shows in a practical way how to design a **scientific and data-driven** cryptocurrency portfolio.

---

If you want:
✔ I will write an English version
✔ I can also add **Installation**, **Usage**, or **Sample Plots** sections for GitHub
✔ I will even create a project logo or badge

Just tell me ❤️
