# ChurnQuest: Navigating the Waves of Customer Retention in Telecommunications

## 📌 Project Overview
This repository contains a comprehensive data analytics project aimed at identifying, analyzing, and predicting customer churn for **Airtel**, a leading telecommunications company. By examining subscriber usage behaviors, billing charges, and customer support patterns, this project builds data-driven solutions to isolate the primary triggers of customer attrition and provides actionable strategies to improve customer retention.

---

## 🛠 Tools & Technologies
The entire analytical workflow was constructed in **Jupyter Notebook** using an end-to-end Python data science pipeline:
* **Data Manipulation & Processing:** `Python 3`, `Pandas`, `NumPy`
* **Statistical Analysis & Modelling:** `SciPy (Stats)`, `Scikit-Learn` (Logistic Regression, K-Means Clustering, StandardScaler)
* **Data Visualization:** `Matplotlib`, `Seaborn`

---

## 📋 Project Requirements & Prerequisites
To run the analysis scripts locally, ensure you have a Python environment setup with the following dependencies installed:

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn
```

### Dataset Structure
The analysis relies on the **Kaggle Customer Churn Prediction 2020** dataset, which includes the following features:
* **Demographics / Subscriptions:** State, Area Code, Account Length, International Plan (Yes/No), Voice Mail Plan (Yes/No).
* **Usage Metrics:** Call minutes, call counts, and financial charges segmented across **Day, Evening, Night, and International** slots.
* **Customer Friction:** Total number of customer service calls.
* **Target Variable:** `Churn` (Yes/No).

---

## ⚡ Challenges Faced & Technical Solutions

### 1. Hard Chronological Timestamps Absence
* **Challenge:** The dataset lacked explicit date or time fields, making a standard time-series seasonal decomposition impossible.
* **Solution:** Used `account_length` (customer tenure) as a logical lifecycle proxy, segmenting accounts into 5 equal-sized chronological lifespans (`pd.qcut`) to observe churn variance across subscriber lifecycle horizons.

### 2. Missing Categorical Customer Service Call Reasons
* **Challenge:** The database did not capture specific granular reasons for customer calls (e.g., technical failure, billing complaints).
* **Solution:** Used total service call volume as a predictive mathematical proxy, isolating the precise call threshold numbers where attrition probability spikes exponentially.

### 3. Feature Scaling Disparities in Clustering
* **Challenge:** Features like talk minutes had a much higher absolute magnitude than customer service calls, causing distance-based clustering algorithms to heavily lean towards usage features.
* **Solution:** Standardized all inputs using `StandardScaler` to ensure tenure, service calls, and billing cycles contributed equally to the unsupervised `K-Means` profiles.

### 4. Categorical Evaluation Warning in Pandas GroupBy
* **Challenge:** Running aggregations over newly cut categorical variables triggered an automated `FutureWarning` due to deprecated group observation mappings.
* **Solution:** Explicitly enforced the parameter configuration `observed=False` inside pandas `.groupby()` loops to achieve future-proof code executions.

---

## 📊 Core Analytical Insights

* **The Customer Service Tipping Point:** A distinct risk inflection point occurs when a customer crosses **3 support calls**. Churn rates surge exponentially for subscribers in this high-frequency bracket, confirming that unresolved service queries directly trigger churn.
* **The High-Usage Billing Trap:** The day billing structure is strictly linear (a flat rate per minute with no cost ceilings). Consequently, your heaviest daytime talk-volume users face steep billing fees, making them highly susceptible to leaving for competitors offering unlimited plans.
* **Value-Added Feature Stickiness:** Subscribers with an active voicemail plan who actively receive messages showcase a significantly lower churn rate. Utilizing cross-functional network services acts as an operational anchor that increases overall customer stickiness.
* **Revenue Bleed Impact:** Financial evaluations confirm a major risk: the Average Revenue Per User (ARPU) of the churned cohort is noticeably high. Airtel is systematically losing high-spending users, which creates a substantial impact on core profitability.

---

## 💡 Strategic Recommendations for Improvements

### 1. Introduce Automated Support Escalation Thresholds
Implement an automated flag in the CRM system for any subscriber making their **3rd customer service call** within a billing cycle. Route these users immediately to a specialized customer retention squad to resolve complaints before the customer defects.

### 2. Launch Tiered Capped Daytime Talk Bundles
Redesign daytime tariff architectures to include capped or unlimited daytime talking tiers for high-volume corporate and retail users. Providing cost predictability protects high-spending accounts from bill shock and deters them from moving to competitors.

### 3. Target "High International Usage" Plan Upgrades
Proactively reach out to users who log high international usage without an international plan. Offer them customized, bundled roaming plans to lower their pay-as-you-go costs while locking in a steady subscription fee for Airtel.

### 4. Incentivize Voicemail Adoption
Run promotional campaigns to encourage voicemail activation among users who do not have it. Bundling value-added services increases digital touchpoints, deepens network utility, and naturally drives down churn rates.
