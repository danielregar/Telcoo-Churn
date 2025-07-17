# 📦 Telco Customer Churn Analysis
**End-to-End Analytics Project (2018–2024)**

This project investigates customer churn at a telecom company using data from 15,000 customers. 

The goal is to identify churn drivers, quantify financial impact, and provide actionable insights for Marketing, Product, Finance, and Customer Success teams.

---
## 📊 Dataset Overview

**Total Customers**: 15,000  
**Period**: 2018–2024  
**Target Variable**: `Churn Label (Yes/No)`  
**Data Sources**:
- Demographics: Gender, Age, Senior Citizen, Marital Status, Dependents
- Location: Zip code, State, City, Lat/Long
- Population Estimates
- Services: Internet, Phone, Streaming, Bundles, Usage, etc
- Status: Satisfaction Score, CLTV, Churn Reason, etc

📎 All tables are joined by `CustomerID`.

---

## 🎯 Project Objectives

- Identify why customers churn
- Segment high-risk users
- Estimate revenue loss from churn
- Recommend business interventions backed by data

---

## 🔧 Data Cleaning Summary

As part of the preprocessing, I tracked data issues and resolutions.  
You can view the full log here:

📋 [Data Cleaning Log (Google Sheet)](https://docs.google.com/spreadsheets/d/1NUHW3IfGE2hdnCHMLYw6rr7DodrnKHV9gZan9wur9eQ)

---
## 🔍 Key Business Questions

### Marketing
- Which customer segments have the highest churn?
- Do offers or referrals reduce churn?
- Which contract types retain better?

### Product
- Which services reduce churn risk?
- Are bundle users more loyal?
- Are customers churning due to dissatisfaction?

### Finance
- How much revenue is lost due to churn?
- What’s the average time before churn?
- If churn drops by 5%, how much do we gain?

### Customer Success
- Can we predict who will churn next quarter?
- Are there early warning signs before churn?
- Do churned customers show low satisfaction?

---


# 🧠 Executive Summary 

Customer churn in this telecom dataset is not strongly predicted by any single demographic, though **senior citizens** and those with **0 dependents** account for the highest churn volume due to their population size. The highest churn **rate** occurs among **new users with 1-year contracts (27%)**, signaling issues with onboarding and early satisfaction. **Referral** and **offer programs** show *no measurable impact* on retention (p > 0.4). Product usage, including services like **streaming, backup, or security**  does **not reduce churn**, and **bundle users (3–9 services)** churn at similar rates, showing no loyalty advantage. While **satisfaction scores** remain flat, **churn reasons** clearly point to dissatisfaction: _“Too expensive,” “Poor service,”_ and _“Found better deal”_ dominate.

Financially, churned customers have already generated **$8.4M** in revenue, but we’ve lost an additional **$13.6M** in projected Customer Lifetime Value (CLTV),  **20.3%** of the total opportunity. Notably, **high-value segments** are also affected: over **330 customers** in the **$6000–6999 CLTV tier** have churned. On average, churn occurs after **39 months**, meaning we’re losing **long-term, high-value customers**.

Reducing churn by just **5%** (747 customers) would retain an estimated **$3.35M**, with each 1% drop in churn saving **~$670K** in future value. Even without machine learning, simple rule-based logic reveals high-risk churn profiles: **new users with 1-year contracts**, **early users with 2-year contracts**, and those with **Bundle Score = 5**. While short tenure users churn faster, the bulk of churn comes from **long-tenure users**, underscoring the need for proactive retention strategies and more effective satisfaction monitoring beyond static surveys.


# 🎯 Insights
## 🧩 1. Marketing
### 1.1 Which customer segments have the highest churn?
I explored churn from multiple angles = age, city, family status, and more,  to uncover where loss is concentrated.

#### 1.1.1 Age Group
<img width="676" height="266" alt="image" src="https://github.com/user-attachments/assets/b59d22a1-796c-48b8-ab12-23336dbf8912" />


**Senior citizens** (**65**+) account for the **highest churn volume** (**920** churned), not because they’re riskier, but because they represent a large portion of the base. 

Their churn rate? A consistent **20–21**%, just like others.


#### 1.1.2 Number of Dependents

<img width="682" height="287" alt="image" src="https://github.com/user-attachments/assets/91f3d48a-1667-42e2-9ff2-c3fe69b64173" />

- Customers with **0 dependents** form the **largest customer group (9,375)** and also account for the **highest churn volume (21%).**
- Churn volume among customers with **1–3 dependents is relatively balanced**, ranging from **350 to 383** churned users.
- The **lowest churn rate (19%)** is seen in customers with **3 dependents**, hinting at slightly stronger loyalty in larger households.
- Overall, the Number of Dependents does not appear to be a strong driver of churn.

#### 1.1.3 City

<img width="613" height="282" alt="image" src="https://github.com/user-attachments/assets/1f69f29e-1221-4717-abb5-4496e4d2133c" />

- Churn rates are **remarkably consistent across cities**, ranging from **19% to 22%.**
- **Miami** shows the **highest churn rate**, while **New York** and **Seattle** have the **lowest** (**19**%), but the gap is minimal.
- Overall, location does not appear to be a strong driver of churn.
#### 1.1.4 Married Status

<img width="627" height="275" alt="image" src="https://github.com/user-attachments/assets/b2f47618-739b-4757-a6fa-6e79b67a55d6" />


- Whether a customer is **married or not** makes **little difference in churn behavior**.
- Churn percentages are **nearly identical** between married and unmarried customers, showing no **predictive power** in this variable.

### Extra Findings
#### Cross-Segment Insight: Churn by Tenure + Contract

| Tenure      | Tenure Group |
| -------------- | ------------- |
| <=6       | New       |
| Between 7 and 12    | Early         |
| Between 13 and 24   | Established       |
| Between 25 and 48   | Loyal        |
| >48  | Very Loyal       |

By grouping customers by tenure and contract type, we surfaced more actionable insights:

- **New customers** (**≤6 months**) with **1-year contracts** churn at **27**%, our **highest-risk group**.
- **Early churn** is often tied to poor onboarding or an unclear value proposition.
- **Very loyal customers** (**>48 months**) and **loyal customers**(**25–48 months**) still make up the majority of total churn volume by difference contract.
- Even tho their churn percentage is not as high **27**%, around **20-21%** but this shows our loyal and very local customer is also churned.
- Retention strategy must target both ends of the customer journey

### 1.2 Do offers or referrals reduce churn?

Tested this with a **Chi-Square analysis**:

🎁 Offers → **p-value = 0.42**

🙋 Referrals → **p-value = 0.44**

**Conclusion**: No statistically significant effect.

Acquisition incentives like offers or referrals **do not influence long-term retention**. 

### 1.3 Which contracts retain better?
<img width="630" height="335" alt="image" src="https://github.com/user-attachments/assets/cae68c63-0a29-4847-a74f-ec3eee93e8ee" />

- Surprisingly, **Month-to-Month customers**, often seen as risky, show the **lowest churn** (**20**%)
- Both **1-Year and 2-Year contracts churn at 21%**, despite longer commitments
- Contract type alone doesn’t guarantee loyalty.

## 🛠 2. Product
### 2.1 Do specific services reduce churn?

**Not really**. Whether a customer has:
- Online Security
- Streaming Services
- Backup or Protection Plans
- etc

The churn rate stays around **20–21%** across the board. No single service adds “stickiness”.

### 2.2 Are bundle users more loyal?

<img width="637" height="297" alt="image" src="https://github.com/user-attachments/assets/136ad412-ba2c-4c13-a438-15c87036d21b" />

Bundles do not equal loyalty. 

The churn across the bundle scores is pretty much the same, around 19-21%. Even highly engaged users can churn. Retention must address why customers leave, not just how much they use.
- Most churned customers have a bundle score between **4–6**.
- The highest churn count is at score **5 (799 churned)**.
- Scores **1, 9, 10 show very low churn**, but their sample size is tiny.
- The dotted line is the average churn volume (**278**), and most mid-range bundle scores are above that line.


### 2.3 Are customers churning due to dissatisfaction?

<img width="634" height="364" alt="image" src="https://github.com/user-attachments/assets/975e0d7f-ebd8-4730-806d-281971d44413" />


At first glance, no, the satisfaction score is flat across churned and retained users.
But **churn reasons**? A different story.

**💸 “Too expensive” – 651**

**🧩 “Poor service” – 596**

**🔄 “Found better deal” – 599**


Customers are leaving due to **price sensitivity, service quality, and competitive alternatives**, not necessarily low survey scores. Satisfaction surveys may be lagging indicators; churn reasons are real-time signals.

## 3.💰 Finance
### 3.1 How much revenue is lost due to churn?

| Metric      | Amount |
| -------------- | ------------- |
| Revenue from churned users       | $8.4M       |
| CLTV lost from churn    | **$13.6M**         |
| Total projected CLTV   | $67.3M        |

Churn has **already cost us $13.6M in future value** — a **20.3%** **revenue leak** that we cannot recover unless churn slows down.

##### 3.1.1 Are we losing high-value Customers?

<img width="625" height="376" alt="image" src="https://github.com/user-attachments/assets/72469de6-b173-402a-a3f2-47166ed3076e" />

Across nearly all CLTV categories, churn rates are consistently **high**, including among customers valued at **over $5000**.
We’ve **lost hundreds of high-value customers**, with the **$6000–6999** segment showing **333** churned users, **one of the highest overall.**

We're not just losing low-value users, we're **losing top-tier customers** who represent the most financial risk.

### 3.2 What’s the average time before churn?
📉 **39 months** or over 3 years of service before they leave.

We’re not just losing new users. We’re losing **long-tenured, high CLTV customers.** This makes churn even more expensive.

### 3.3 What if we reduce churn by just 5%?

🎯 Target: drop churn from **20.4**% → **15.4**%

📉 Saves: **747 customers**

💸 Gain: **$3.35M** in retained lifetime value

That’s ~$670K per percentage point. Even a small drop pays huge dividends.

## 🤝 4. Customer Success
### 4.1 Can we predict who will churn next quarter?

**Yes** — even without machine learning.

Rule-based logic shows clear high-risk profiles:

- **New customers + 1-year contracts** → **27**% churn
- Early customers (**7–12 months**) + **2-year contracts** → **23**%
- Customers with **5 bundled services** → **22**% churn and **highest volume**

Flagging these groups now means retention teams can act early.

### 4.2 Are there early warning signs?

**Yes**, but not just in new users.

While short-tenure customers do churn faster, the highest churn volume comes from **long-tenure segments**:

- Loyal customers (**25–48 months tenure**)
- Very loyal customers (**>48 months**)

- These groups have more customers churning in total than new users, meaning we're **losing users who stayed with us for years**.

Other churn signals:

- Short-tenure customers do churn at a higher rate, even by a small difference, but they’re a smaller portion of total churn
- A high number of bundled services doesn't ensure retention — some heavily subscribed users still leave
- Early warning signs include not just new user drop-off, but also long-term fatigue, unmet expectations, and dissatisfaction building over time.

## 4.3 Do churned customers show low satisfaction?

**Only in what they say, not in what they score.**
- Satisfaction score: **flat**
- Churn reasons: loud and clear

This shows a gap between survey data and real behavior, and validates churn reason as the more reliable metric.

# 🔧 Recommendations
While churn patterns appear steady across demographics and services, the real reasons customers leave are loud and consistent:

**💸 “Too expensive”**

**🧩 “Poor service”**

**🔄 “Found better deal”**

These aren’t random, they’re a clear signal that perceived value is not meeting customer expectations. 

Customers aren't just walking away due to features, contracts, or demographics, they’re leaving because the experience, pricing, or support fails to justify staying.


To address the root causes of churn and retain high-value customers:

**- Reposition pricing with value tiers**

Introduce clearer, more flexible pricing that aligns with usage or tenure, especially for customers at risk of price sensitivity.

**- Improve the early onboarding experience**

The highest churn rate (27%) occurs in new customers with 1-year contracts. Deliver stronger onboarding, early check-ins, and welcome incentives.

**- Launch a churn-reduction program focused on loyal customers**

Long-tenured users (25+ months) make up the majority of churn volume. Proactively engage them with loyalty rewards, plan reviews, or retention calls.

**- Monitor churn reasons continuously**

Satisfaction scores alone are not enough. Build a live feedback loop from cancellation forms or support tickets to track real-time sentiment.

**- Competitive benchmarking & retention offers**

highlight advantages over competitors and provide upgrade incentives before the contract ends

## 🤖 Predictive Modeling
While this project relied on rule-based logic, churn prediction can be extended using:
- Logistic Regression for explainability


