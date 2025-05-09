README.txt
==========

Title: Resource Allocation in 5G Networks using Game Theory  
Author: Megha Iyengar  
Institution: Arizona State University  
Date: May 2025  
Repository: https://github.com/meghabyte-og/5g-resource-allocation-game-theory  

Overview
--------
This repository presents a complete implementation of a game-theoretic framework for modeling resource competition in 5G networks. Each user is modeled as a rational agent competing for bandwidth and low-latency access, choosing between a high-demand and a fallback strategy. The model uses real-world quality-of-service (QoS) data to define user payoffs, and solves for mixed-strategy Nash equilibria using best-response dynamics. All code and data processing is implemented in Julia and Python.

Game Description
----------------
The interaction among users is modeled as a non-cooperative strategic-form game:

- **Players:** Users \( i \in \{1, 2, \dots, N\} \) in a 5G network.
- **Strategies:** Each user selects a strategy \( S_i = (b_i, l_i) \), representing their requested bandwidth and latency, constrained as:
  \[
  B_{\min} \leq b_i \leq B_{\max}, \quad L_{\min} \leq l_i \leq L_{\max}
  \]
  Practically, each player chooses between:
  - A **high-demand** profile \( (b_i^{\text{obs}}, l_i^{\text{obs}}) \) from the dataset
  - A **fallback** profile \( (b_i^{\text{low}}, l_i^{\text{low}}) \) with minimal bandwidth and relaxed latency

- **Payoffs:** Each player receives a QoS-based utility:
  \[
  \pi_i = \alpha_j \cdot \text{AllocatedBandwidth}_i \cdot \left(1 - \frac{\text{Latency}_i}{L_{\max}} \right) \cdot \left(1 + \frac{\text{SignalStrength}_i}{S_{\max}} \right) \cdot \text{ResourceAllocation}_i
  \]
  where \( \alpha_j \) is an application-specific weight calculated from the average bandwidth-to-latency ratio.

- **Equilibrium:** Users update their strategy probabilities \( p_i \in [0, 1] \) through a best-response learning process until convergence:
  \[
  p_i^{(t+1)} = (1 - \eta) \cdot p_i^{(t)} + \eta \cdot \text{BestResponse}_i
  \]

File Structure
--------------
- `Quality of Service 5G.csv`: Original Kaggle dataset with raw QoS metrics
- `Cleaned_Quality_of_Service_5G.csv`: Parsed and standardized dataset used for modeling
- `Alpha_Values.csv`: Application-specific scaling factors \( \alpha_j \) for payoff weighting
- `Dataset_With_Payoff.csv`: Dataset with full payoff values computed
- `Mixed_Strategy_Equilibrium.csv`: Final equilibrium strategy probabilities for each user
- `initial-vizualization.ipynb`: Python notebook for exploratory data analysis
- `Project.ipynb`: Main Julia notebook implementing the game-theoretic model, payoff function, and best-response algorithm

Usage
-----
1. Review the cleaned dataset and application weights.
2. Run `initial-vizualization.ipynb` to understand key patterns in latency, signal strength, and bandwidth.
3. Open `Project.ipynb` in Julia to execute the simulation and compute the Nash equilibrium.
4. Inspect `Mixed_Strategy_Equilibrium.csv` to analyze strategy probabilities at equilibrium.

Dependencies
------------
- Julia ≥ 1.8 with `DataFrames`, `CSV`, and standard numerical libraries
- Python ≥ 3.8 with `pandas`, `matplotlib`, and `seaborn` (for visualization)
