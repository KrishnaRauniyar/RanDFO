
#### `docs/usage/stochastic.md`
```md
---
title: Stochastic (Noisy)
parent: Usage
nav_order: 2
---

# Stochastic (noisy)

```python
import numpy as np
from core.solver import DiagHessianStarSolver

def rosenbrock(x):
    return np.sum(100.0*(x[1:]-x[:-1]**2)**2 + (1-x[:-1])**2)

def rosenbrock_noisy(x):
    return rosenbrock(x) * (1.0 + 0.01*np.random.randn())

x0 = np.zeros(10)
options = {"stochastic": True}
solver = DiagHessianStarSolver(f=rosenbrock_noisy, x0=x0, options=options, f_true=rosenbrock)
best = solver.solve()
