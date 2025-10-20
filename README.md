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

#### Step 2 – Monte Carlo Simulation

The core of the project.
For each agent, the script repeatedly draws random samples of increasing sizes (from 30 up to the agent’s total observations).

Each draw computes:

- Sample size (n)

- Verification rate (mean(verified_status))

This iterative sampling simulates how verification stability behaves as sample size increases — mimicking real-world variability.

#### Step 3 – Aggregation and Statistical Tests

After running the simulations:

- Results are aggregated to measure mean and standard deviation of verification rates at each sample size.

- Correlation tests (cor.test) assess whether larger sample sizes produce more stable (less volatile) verification rates.

- Country-level and global linear models (lm) summarize the overall relationship.

#### Step 4 – Visualization

The /Images folder contains key plots generated from the simulation:

| Visualization                    | Description                                                                            |
| -------------------------------- | -------------------------------------------------------------------------------------- |
| **stability_plot.png**           | Shows how verification rate variability (std. dev.) decreases as sample size increases |
| **correlation_distribution.png** | Displays distribution of correlation coefficients per agent                            |
| **significant_agents.png**       | Highlights agents with statistically significant relationships (p < 0.05)              |
| **country_relationship.png**     | Compares trends across countries via linear fit lines                                  |


### ✨✨ Sample outcome
#### 1️⃣ Verification Stability vs Sample Size
📌Larger sample sizes exhibit smaller standard deviations in verification rate — confirming that larger samples stabilize performance metrics.


#### 2️⃣ Correlation Distribution
📌This plot shows how the relationship between sample size and verification rate varies across agents.


#### 3️⃣ Country-Level Trends
📌Agents with statistically significant correlations (p < 0.05) between sample size and verification rate are visualized below:


### 📈 Results Summary
Country	Avg Correlation	% Significant
| Country    | Avg Correlation | % Significant |
| ---------- | --------------- | ------------- |
| Nigeria    | 0.45            | 62%           |
| Malawi     | 0.38            | 55%           |
| Mozambique | 0.41            | 58%           |
| Madagascar | 0.47            | 60%           |


   (Example output — generated when you run the script.)

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
 🔗![PenguPudgyGIF](https://github.com/user-attachments/assets/520f7c8b-0440-4083-ac56-5e1acc826d1b)
