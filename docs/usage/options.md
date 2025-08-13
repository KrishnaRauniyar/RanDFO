---
title: Options
parent: Usage
nav_order: 4
---

# Solver Options

| Option | Default | Meaning |
|---|---:|---|
| `p` | 2 | Subspace dimension |
| `delta0` | 1.0 | Initial trust-region radius |
| `delta_max` | 5.0 | Maximum trust-region radius |
| `delta_end` | 1e-6 | Termination radius (if used) |
| `eta1` | 0.01 | Accept step threshold (low) |
| `eta2` | 0.9 | Accept step threshold (high) |
| `gamma` | 2.0 | Radius shrink/expand factor |
| `r` | 1.0 | Model regularization / scaling (if applicable) |
| `jlm_type` | 3 | Subspace basis type (identity, Haar, scaled Haar, hashing…) |
| `max_eval` | 1000 | Max function evaluations |
| `max_iters` | 100 | Max iterations |
| `mc_samples` | 1 | Monte-Carlo samples per estimate |
| `parallel` | False | Use joblib parallelism |
| `cpu` | 1 | Cores for parallelism |
| `adaptive_subspace` | False | Enable p-expansion after failures |
| `stochastic` | False | Treat objective as noisy |
| `seed` | 42 | RNG seed |

### Example
```python
options = {
    "p": 2, "delta0": 1.0, "delta_max": 5.0,
    "eta1": 0.01, "eta2": 0.9, "gamma": 2.0,
    "jlm_type": 3, "max_eval": 1000, "max_iters": 100,
    "mc_samples": 1, "parallel": False, "cpu": 1,
    "adaptive_subspace": False, "stochastic": False, "seed": 42
}
