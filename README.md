# Analyzing Heterogeneous Effects of Loss-vs-Gain Framing with Causal Machine Learning

This repository contains an R-based analysis script that applies Causal Machine Learning (Causal Forests) to investigate the heterogeneous treatment effects of **loss-framed** versus **gain-framed** messaging. The analysis aims to optimize user conversion and payment amounts by identifying which psychological framing works best for specific user subgroups.

## Project Overview

*   **Goal:** Determine optimal communication strategies (Loss vs. Gain) for maximizing pension/contract payments.
*   **Methodology:** Generalized Random Forests (via the `grf` package).
*   **Data Split:** Temporal validation (Training on 2021 data, Testing on 2022 data).

## Key Components

### 1. Data Processing & Randomization Checks
*   Loads participant data. Data is only available for the review process. 
*   Defines covariates including demographics (`gender`, `age`), financial status (`contract_valuation`, `historical_payments`), and skills (`management_skills`).
*   Validates randomization balance using summary statistics.

### 2. Causal Model Training
Two distinct Causal Forest models are fitted:
1.  **Extensive Margin Analysis:** Binary outcome (Did the user pay?).
2.  **Intensive Margin Analysis:** Continuous outcome (How much did the user save?).

### 3. Heterogeneity Analysis (CATE & GATE)
The script moves beyond Average Treatment Effects (ATE) to explore Conditional Average Treatment Effects (CATE):
*   **GATE (Group Average Treatment Effects):** Analyzes treatment impact across specific groups:
    *   **Gender**
    *   **Contract Valuation** (Proxy for wealth)
    *   **Management Skills** (Financial literacy)
*   **Visualizations:** Includes calibration histograms, TOC (Targeting Operator Characteristic) curves, and quartiled heterogeneity plots.

### 4. Policy Evaluation & Economic Impact
Simulates the impact of deploying a Causal ML-based policy:
*   Compares the **Optimal Policy** (assigning treatment based on CATE sign) against baselines:
    *   Random Assignment
    *   "All Loss" Strategy
    *   "All Gain" Strategy
*   Demonstrates potential lifts in conversion rates and total payment volume.

### 5. Explainable AI (XAI)
Interprets the "black box" Causal Forest using:
*   **Variable Importance:** Identifies drivers of heterogeneity (e.g., *Contract Valuation*).
*   **SHAP Values:** Bee-swarm plots to visualize feature contributions.
*   **Partial Dependence Plots (PDP):** Visualizes the marginal effect of key features on the estimated treatment effect.

### 6. Robustness Checks
Validates ML findings against traditional econometric methods:
*   **Probit Models:** For binary conversion margins.
*   **OLS:** For payment amounts.
*   **Heckman Two-Step Selection:** To correct for selection bias (extensive vs. intensive margin) in payment amounts.
