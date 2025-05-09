# Resource Allocation in 5G Networks using Game Theory
**Author:** Megha Iyengar   
**Repository:** https://github.com/meghabyte-og/5g-resource-allocation-game-theory

---

## Overview

This repository implements a game-theoretic model to simulate resource competition in 5G wireless networks. Each user is modeled as a rational agent competing for bandwidth and low-latency service. The model uses real-world QoS data to define user payoffs and computes a mixed-strategy Nash equilibrium using best-response dynamics. All components are implemented in Julia and Python.

---

## Game-Theoretic Model Description

The resource allocation problem is modeled as a **strategic-form game**:

- **Players:**  
  A finite set of users *i ∈ {1, 2, ..., N}*, each independently choosing resource requests.

- **Strategies:**  
  Each user *i* selects a pair *(bᵢ, lᵢ)* of requested bandwidth and latency, constrained by:


B_min ≤ bᵢ ≤ B_max
L_min ≤ lᵢ ≤ L_max


Each user chooses between:
- A **high-demand profile** *(bᵢ^obs, lᵢ^obs)* (from empirical data)
- A **fallback profile** *(bᵢ^low, lᵢ^low)* (minimal bandwidth, relaxed latency)

The user applies a **mixed strategy**, selecting the high-demand profile with probability *pᵢ ∈ [0, 1]*.

- **Payoff Function:**

Each user's QoS-driven utility is defined as:

πᵢ = αⱼ × AllocatedBandwidthᵢ × (1 − Latencyᵢ / L_max) × (1 + SignalStrengthᵢ / S_max) × ResourceAllocationᵢ

where:
- *αⱼ* is an application-specific weight derived from bandwidth-to-latency ratio
- *AllocatedBandwidthᵢ* depends on total demand
- *Latencyᵢ*, *SignalStrengthᵢ*, and *ResourceAllocationᵢ* are drawn from the dataset

The expected utility is computed via Monte Carlo sampling over strategy combinations.

- **Equilibrium Computation:**

Users update strategy probabilities *pᵢ* iteratively using best-response dynamics:

pᵢ(t+1) = (1 − η) × pᵢ(t) + η × BestResponseᵢ

where η is the learning rate, and `BestResponseᵢ` is determined by comparing expected payoffs of the two profiles.

---

## File Structure

- `Quality of Service 5G.csv` – Raw dataset (Kaggle)
- `Cleaned_Quality_of_Service_5G.csv` – Parsed and standardized data
- `Alpha_Values.csv` – Application-specific scaling factors
- `Dataset_With_Payoff.csv` – Dataset with payoff values added
- `initial-vizualization.ipynb` – Python EDA notebook
- `Project.ipynb` – Julia implementation of the game-theoretic model

---

## How to Run

1. Clone the repository.
2. Open `initial-vizualization.ipynb` to review data trends and correlations.
3. Run `Project.ipynb` using Julia to simulate payoffs and compute the Nash equilibrium.
4. Inspect `Mixed_Strategy_Equilibrium.csv` for final strategy probabilities.

