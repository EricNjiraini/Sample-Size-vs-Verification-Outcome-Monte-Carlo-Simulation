# Effect of Sample Sizes on Verification Rates across Multiple Markets
## Author: Eric Njiraini

# 🎯 Overview
This repository explores how **sales sample size impacts sales verification rate and its stability** using a **Monte Carlo simulation** approach.  
Originally designed for commercial verification analysis, this method also applies broadly across:
- 🏦 **Finance** – understanding stability of credit verification or audit samples  
- 🏥 **Healthcare** – modeling diagnostic test reliability across sample sizes  
- 🛒 **Commercial operations** – optimizing customer verification or quality control samples  
The project demonstrates how sampling variability affects performance reliability and provides a reproducible framework to **estimate the minimum sample size needed for stable verification rates**.
---

### 🧠 Simulation Logic
#### Step 1 – Load & Prepare Data

- Data can be pulled from a source of your choice or loaded locally (CSV).
- Once loaded, basic cleaning ensures that only sampled and verified cases are included for analysis.
- Key preprocessing steps include:
  - Filtering out unsampled or uncontacted records
  - Creating binary indicators (call_status, verified_status)
  - Converting to data.table format for efficient computation
  - Ensuring each agent has a sufficient number of records (≥30)
  - 
#### Step 2 – Monte Carlo Simulation

The core of the project.
For each agent, the script repeatedly draws random samples of increasing sizes (from 30 up to the agent’s total observations).

Each draw computes:

- Sample size (n)

- Verification rate (mean(verified_status))

This iterative sampling simulates how verification stability behaves as sample size increases — mimicking real-world variability.

#### Step 3 – Aggregation and Statistical Tests

After running the simulations:

- Results are aggregated to measure the mean and standard deviation of verification rates at each sample size.

- Correlation tests (cor.test) assess whether larger sample sizes produce more stable (less volatile) verification rates.

- Country-level and global linear models (lm) summarize the overall relationship.
  
---
### Outcome and Interpretation

#### Data Visuals 

1. **Stability/Variability:**
- Verification rate stability improves with larger sample sizes.
- The stability plot demonstrates a key principle from the Central Limit Theorem (CLT) — as the sample size increases, the variability of the verification rate (represented by the standard deviation) decreases.
- In other words, larger sample sizes yield more stable and reliable estimates of the true verification rate, while smaller samples are more prone to random fluctuation.
- This inverse relationship between sample size and variability supports inferential reliability: decisions or performance evaluations based on larger samples are statistically more robust than those based on smaller ones.
- The curve visually highlights how sampling uncertainty diminishes with size — a practical reminder that consistency improves as we approach population-level representation.
  
![stability_plot](https://github.com/EricNjiraini/Sample-Size-vs-Verification-Outcome-Monte-Carlo-Simulation/blob/main/Images/overall_verification_stability_vs_sample_size.png)

2. **correlation Distribution:**
- Most agents exhibit a negative correlation between sample size and volatility
- The histogram shows that as the sample size grows, the verification rate becomes more predictable. This consistent negative skew suggests that expanding the sample size enhances reliability across agents

![correlation_Distribution](https://github.com/EricNjiraini/Sample-Size-vs-Verification-Outcome-Monte-Carlo-Simulation/blob/main/Images/correlation_distribution.png)

3. **Country-level comparison of verification rate dynamics.**
- The regression lines illustrate that while baseline verification rates differ by country, the trend (improved stability with larger samples) is consistent across all. This suggests the sampling effect is structural, not country-specific.

[Country-level comparison](https://github.com/EricNjiraini/Sample-Size-vs-Verification-Outcome-Monte-Carlo-Simulation/blob/main/Images/country_relationship.png)

### Model summary
#### Model Summary (Linear Model)
| Predictor         | Estimate | Std. Error | t value | p-value | Interpretation                                                                                                                    | Estimated Verification Rate |
| ----------------- | -------- | ---------- | ------- | ------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------- |
| (Intercept)       | 0.950    | 0.00118    | 802.51  | <0.001  | **Baseline verification rate** for agents in **Madagascar** (reference).                                                          | **0.950**                   |
| sample_size       | -0.00036 | 0.00000    | -141.86 | <0.001  | Each additional sampled record slightly reduces verification rate — suggesting diminishing marginal verification as samples grow. | —                           |
| countryMALAWI     | -0.268   | 0.00123    | -217.28 | <0.001  | Agents in **Malawi** have a **26.8% lower** verification rate than those in Madagascar.                                           | **0.950 − 0.268 = 0.682**   |
| countryMOZAMBIQUE | -0.246   | 0.00123    | -199.94 | <0.001  | Agents in **Mozambique** have a **24.6% lower** verification rate than Madagascar.                                                | **0.950 − 0.246 = 0.704**   |
| countryNIGERIA    | -0.081   | 0.00120    | -67.43  | <0.001  | Agents in **Nigeria** show an **8.1% lower** verification rate relative to Madagascar.                                            | **0.950 − 0.081 = 0.869**   |

#### Model Fit
- Residual Std. Error: 0.162
- R²: 0.25
- F-statistic: 78,070 , p < 0.001

#### Summary
- Madagascar shows the highest expected verification rate (~95%), serving as the performance benchmark.
- Nigeria follows closely (~87%), indicating relatively strong verification consistency.
- Mozambique (~70%) and Malawi (~68%) trail behind, suggesting lower verification effectiveness or operational differences.
- The small but significant negative coefficient on sample size indicates that as sample size increases, the verification rate slightly decreases—likely due to reaching harder-to-verify cases as the pool broadens.
- The model thus quantifies both country-level verification efficiency and the marginal effect of sample size, reinforcing that larger samples yield stable but slightly lower mean verification rates.

### 💼 Use Cases
#### Domain	Example
1. Finance	Assess credit verification stability vs sample size
2. Commercial Ops	Determine optimal sampling effort for QA or survey verification
3. Healthcare	Quantify diagnostic verification reliability across patient samples

### 🤝 Contributing

Contributions are welcome — if you adapt this approach to a new domain or extend the model, open a pull request!

📜 License

MIT License © 2025 Eric Njiraini

💡 Author

Eric Njiraini
Data Analytics Lead | MSc Data Science (UEL)

 [LinkedIn](https://www.linkedin.com/in/eric-njiraini/)
 ![PenguPudgyGIF](https://github.com/user-attachments/assets/520f7c8b-0440-4083-ac56-5e1acc826d1b)
