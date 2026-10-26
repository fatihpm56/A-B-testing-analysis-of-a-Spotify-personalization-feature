# 🎧 Spotify Campaign A/B Test Analysis

An A/B testing analysis evaluating a new personalization feature/algorithm (**Target**) against the existing experience (**Control**) on a music streaming platform, followed by post-implementation monitoring after full rollout.


## 📌 Project Overview

| Item | Detail |
|---|---|
| Objective | Test whether the Target variant improves engagement, listening duration, payment conversion, and Premium upgrades |
| Sample | 100,000 users (50,000 Control vs 50,000 Target) |
| Randomization unit | Per user |
| Primary metric | Payment Rate |
| Supporting metrics | Engagement, Duration Played, Premium Rate |
| Significance level | α = 5% |

**Hypotheses**
- H0: There is no difference in the mean/proportion of the metric between Target and Control.
- H1: The mean/proportion of the metric is higher in Target than in Control.

## 📂 Datasets

- `spotify_campaign_data.csv`: user-level experiment data with group (Control/Target), Engagement score, Duration Played (minutes), Payment, and Subscription tier.
- `AB_Test_Post_Implement.csv`: daily Total Users from 1–15 March 2026, used for post-implementation monitoring.

## 🔬 Methodology

- **Welch's t-test** for continuous metrics (Engagement, Duration Played)
- **Two-proportion z-test** for binary metrics (Payment, Premium)
- **Cohen's d** for effect size
- **Confounding check** across subscription tiers (Free vs Premium)
- **Linear regression** for the post-implementation Total Users trend

## 📊 Key Results

<img width="889" height="396" alt="image" src="https://github.com/user-attachments/assets/96944adf-8896-473b-9298-72bbdbf141e6" />

<img width="590" height="409" alt="image" src="https://github.com/user-attachments/assets/0228aa31-0a15-4bfa-9441-2935547687b2" />

<img width="690" height="390" alt="image" src="https://github.com/user-attachments/assets/f1536dd8-7c13-499f-93a6-3684d680438e" />


| Metric | Control | Target | Difference | p-value |
|---|---|---|---|---|
| Engagement (mean) | 0.600 | 0.800 | +0.200 (+33.3%) | < 0.001 |
| Duration Played (min) | 120.1 | 159.9 | +39.8 (+33.2%) | < 0.001 |
| Payment Rate | 69.7% | 79.8% | +10.1 pp (+14.5%) | < 0.001 |
| Premium Rate | 59.7% | 80.3% | +20.5 pp (+34.4%) | < 0.001 |

H0 is rejected for all four metrics. Effect sizes are large (Cohen's d ≈ 2.0 for Engagement, ≈ 1.3 for Duration Played). The Payment Rate lift holds across both Free (79.9%) and Premium (79.8%) users in Target, so it is not just a subscription-tier composition effect.

### Post-Implementation Monitoring

<img width="889" height="419" alt="image" src="https://github.com/user-attachments/assets/8aa5808e-1f51-4512-b87c-8aacbe9b50e4" />

| Period | Avg. Users/Day | Change |
|---|---|---|
| Week 1 (1–7 Mar) | 16,184 | baseline |
| Week 2 (8–14 Mar) | 24,670 | **+52.4%** |

The linear trend shows an increase of about +871 users/day (R² = 0.58, p = 0.0009).

## 💡 Recommendations

1. Roll out the Target variant permanently to all users.
2. Prioritize onboarding and communication for Free-tier users to drive Free-to-Premium conversion.
3. Use Payment Rate as the primary metric when reporting to business stakeholders.
4. Continue monitoring for 4–8 weeks to confirm the lift is sustained and not a novelty effect, and track guardrail metrics (churn, user complaints, server load).
5. Verify that no other campaigns or promotions ran concurrently in early March 2026.

## 🛠️ Tech Stack

Python · Pandas · NumPy · SciPy · Statsmodels · Matplotlib · Jupyter Notebook / Google Colab

## 📁 Repository Structure

```
├── data/
│   ├── spotify_campaign_data.csv
│   └── AB_Test_Post_Implement.csv
├── notebook/
│   └── AB testing analysis of a Spotify personalization feature.ipynb
└── README.md
```

## ⚠️ Limitations

- The full-rollout date (8 March 2026) is an analytical assumption.
- The 15-day monitoring window is short; a longer period is needed to confirm a sustained lift.
- Guardrail metrics (churn, complaints, server load) are not covered by this data.
- The post-implementation comparison is a simple before/after, so it cannot fully rule out external factors.

## 👤 Author

**Fatih Putra Maulana**
