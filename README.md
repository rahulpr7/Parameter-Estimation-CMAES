# Parameter Estimation using Hybrid CMA-ES and L-BFGS

This repository presents a **hybrid optimization framework** combining **CMA-ES (Covariance Matrix Adaptation Evolution Strategy)** and **L-BFGS (Limited-memory Broyden–Fletcher–Goldfarb–Shanno)** for solving **non-linear parameter estimation problems** with high accuracy and computational efficiency.

---

## 📘 Overview

The optimization is performed in two stages:

1. **Global Search (CMA-ES):**  
   CMA-ES efficiently explores the entire parameter space to locate a promising region near the global minimum.

2. **Local Refinement (L-BFGS):**  
   Once a good region is identified, the GPU-accelerated L-BFGS optimizer refines the parameters to achieve a high-precision local optimum.

---

## ⚙️ Features

- Hybrid approach combining **exploration** and **fast convergence**
- Supports **non-linear, non-convex** objective functions
- GPU acceleration for **L-BFGS** (via PyTorch)
- Automatic **line search** with **Wolfe conditions**
- Benchmark dataset for reproducibility

---

## 🧮 Methodology

1. **Stage 1 — CMA-ES Optimization**
   - Randomly samples candidate solutions from a multivariate Gaussian distribution.
   - Adapts covariance matrix and step-size over iterations.
   - Identifies a region near the global optimum.

2. **Stage 2 — L-BFGS Optimization**
   - Starts from the CMA-ES best solution.
   - Performs gradient-based refinement using PyTorch’s autograd.
   - Enforces Wolfe condition for descent direction.

---

## 📊 Results Summary

| Optimizer| Iterations | Final Loss   | Time (s) | Estimated Parameters      |
| -------- | ---------- | ------------ | ---------| ------------------------- |
| CMA-ES   | 100        | 0.000263     | 1.23     | 30.0002, 0.030000, 55.0021    |
| L-BFGS   | 200        | 0.000256     | 0.11     | 29.9996, 0.02999, 55.0012     |
| **Total**| **300**    | **0.000256** | **1.34** | **[29.99, 0.03, 55.00]** |


> The hybrid approach achieved 32-bit precision on optimized parameters with a mean ℓ₁ loss of `0.000256`, confirming a high-fidelity fit to the dataset.


