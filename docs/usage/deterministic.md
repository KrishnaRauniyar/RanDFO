---
title: Deterministic
parent: Usage
nav_order: 1
---

# Deterministic (noise-free)

```python
import numpy as np
from core.solver import DiagHessianStarSolver, FrobStarSolver

def rosenbrock(x):
    return np.sum(100.0*(x[1:]-x[:-1]**2)**2 + (1-x[:-1])**2)

x0 = np.zeros(10)
solver = DiagHessianStarSolver(f=rosenbrock, x0=x0)
best = solver.solve()
print(best)
