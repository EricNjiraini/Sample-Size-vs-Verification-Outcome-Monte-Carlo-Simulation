# Effect of Sample Sizes on Verification Rates
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

3. **Country-level comparison.**
- Baseline verification rates differ between the countries in the data, but in every country the spread of verification rates narrows as the sample grows. The stability effect comes from sampling itself, not from how any one country operates.

### Model summary
A linear model of verification rate on sample size, controlling for country (R² = 0.25), shows that baseline verification rates differ significantly between countries (p < 0.001). The effect of sample size on the average rate is very small and its direction varies by country, so the robust finding is about stability rather than level: larger samples give steadier rates.

Country names and country-level rates are not published.

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
Data Analytics Manager | MSc Data Science (UEL)

 [LinkedIn](https://www.linkedin.com/in/eric-njiraini/)
 ![PenguPudgyGIF](https://github.com/user-attachments/assets/520f7c8b-0440-4083-ac56-5e1acc826d1b)
