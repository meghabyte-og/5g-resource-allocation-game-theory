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

### Game Description

**Players:** Users *i* ∈ {1, 2, ..., N} in a 5G network.

**Strategies:** Each user selects a strategy Sᵢ = (bᵢ, lᵢ), where:
- Bₘᵢₙ ≤ bᵢ ≤ Bₘₐₓ
- Lₘᵢₙ ≤ lᵢ ≤ Lₘₐₓ

Each player chooses between:
- A **high-demand** profile (bᵢ^obs, lᵢ^obs) from the dataset
- A **fallback** profile (bᵢ^low, lᵢ^low) with minimal bandwidth and relaxed latency

**Payoffs:** Each player receives a QoS-based utility:

πᵢ = αⱼ ⋅ AllocatedBandwidthᵢ ⋅ (1 - Latencyᵢ / Lₘₐₓ) ⋅ (1 + SignalStrengthᵢ / Sₘₐₓ) ⋅ ResourceAllocationᵢ

where αⱼ is an application-specific weight based on bandwidth-to-latency ratio.

**Equilibrium:** Each user updates their strategy probability pᵢ ∈ [0, 1] via best-response dynamics:

pᵢ(t+1) = (1 - η) ⋅ pᵢ(t) + η ⋅ BestResponseᵢ

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
