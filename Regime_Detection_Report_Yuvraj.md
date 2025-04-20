
# Regime Detection via Unsupervised Learning
---

## Objective

This project aims to segment financial market behavior into distinct regimes using unsupervised learning techniques applied to order book and volume data. The regimes are defined along three behavioral axes:  
1. **Trending vs. Mean-reverting**  
2. **Volatile vs. Stable**  
3. **Liquid vs. Illiquid**

---

## 1. Feature Engineering

Features were extracted from the top 20 levels of the order book (`depth20`) and trade volume (`aggTrade`) data. The following handcrafted features were computed per timestamp:

- **Liquidity & Depth Features:**
  - Bid-Ask Spread  
  - Order Book Imbalance at level 1  
  - Microprice  
  - Cumulative Bid/Ask Quantity (top 20 levels)  
  - Sloped Depth  

- **Price Action & Volatility:**
  - Mid-price Return (log returns)  
  - Rolling Volatility (10s and 30s)  

- **Volume Features:**
  - Volume Imbalance (Buy vs Sell volume)  
  - Cumulative Volume (10s and 30s)  
  - VWAP shift  

These features aim to capture immediate market microstructure dynamics and trading pressure.

---

## 2. Data Normalization and Dimensionality Reduction

- All features were normalized using **Z-score normalization** to ensure scale consistency.
- **PCA** (Principal Component Analysis) was applied to reduce dimensionality and help clustering algorithms focus on the most significant feature directions.

---

## 3. Clustering Approach

Three unsupervised clustering techniques were explored:

- **K-Means Clustering**
  - Optimal number of clusters chosen via Elbow Method and Silhouette Score.
- **Gaussian Mixture Models (GMM)**
  - Provided soft assignment and probabilistic interpretation.
- **HDBSCAN**
  - Captured non-spherical clusters and allowed for noise handling.

**Evaluation Metrics:**
- **Silhouette Score** for cohesion and separation
- **Davies-Bouldin Index** for cluster compactness

---

## 4. Regime Labeling and Analysis

Each timestamp was assigned a regime label using the clustering output. Regimes were interpreted based on feature distribution:

- **Regime A:** Trending, Liquid, Stable  
- **Regime B:** Mean-reverting, Illiquid, Volatile  
- **Regime C:** Trending, Illiquid, Volatile  
- *(Labels are illustrative; real naming is based on actual feature patterns.)*

For each regime, average spread, volatility, microprice trajectory, and volume pressure were analyzed to characterize behavior.

---

## 5. Visualizations

- **t-SNE plots** showed clear clustering in lower-dimensional space.  
- **Time-series plots** overlaid with regime labels highlighted distinct behavioral segments.
- **Heatmaps and Boxplots** compared feature distributions across regimes.

---

## 6. Regime Transition Insights

A Markovian analysis of regime transitions revealed interesting patterns such as:
- Higher probability of switching from volatile to stable regimes after volume spikes.
- Certain regimes were more persistent, while others transitioned frequently.

---

## Conclusion

This study demonstrates that unsupervised learning can effectively capture nuanced market behaviors using well-engineered microstructure features. Regime insights can support strategic trading decisions, risk management, and model adaptation.
