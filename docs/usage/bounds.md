---
title: Bounds
parent: Usage
nav_order: 3
---

# Bounds

```python
import numpy as np
from core.solver import DiagHessianStarSolver

x0     = np.full(10, 0.0)
lower  = np.full(10, -1.2)
upper  = np.full(10,  5.0)
opts   = {"max_eval": 100, "max_iters": 10}

solver = DiagHessianStarSolver(f=rosenbrock, x0=x0, options=opts, bounds=(lower, upper))
best   = solver.solve()
