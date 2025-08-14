---
title: PySTARS
nav_order: 1
has_math: true
---

# PySTARS: Python Implementation of STARS Optimization Algorithms

PySTARS is a Python-based implementation of STARS (Stochastic Trust-region Algorithm in Random Subspaces) for derivative-free optimization. It supports both deterministic and stochastic objective functions, subspace trust-region models, adaptive sampling, and comprehensive logging.

---

## Features

- Deterministic and stochastic objective function support
- Monte Carlo estimation with optional parallelism and caching
- Trust-region based subspace model
- Adaptive subspace expansion logic
- Diagonal Hessian and Frobenius models
- Logging of evaluations, progress, and objective values
- Terminal output with tracking options
- Full bounds support

---

## When to use PySTARS

PySTARS is designed to solve general black-box optimization problems with optional bound constraints:

$$
\min_{x \in \mathbb{R}^n} f(x), \quad
\text{with} \quad
f(x) = \mathbb{E}_{\theta} \left[ f_{\theta}(x) \right],
$$

where the values of the continuously differentiable function
$f : \mathbb{R}^n \to \mathbb{R}$ are available only via
$f_{\theta}$, a stochastically noisy version of $f$, and
$\theta$ is a random variable whose distribution governs the noise.

PySTARS is a **derivative-free optimization algorithm**, meaning it does not require the user to provide gradients of \( f(x) \), nor does it attempt to estimate them via finite differencing.

### Recommended scenarios
- **Noisy objectives** — when repeated evaluations at the same \(x\) yield different values (e.g., Monte Carlo simulations, stochastic processes, or physical experiments).
- **Expensive evaluations** — when calculating finite-difference gradients would require many costly evaluations.
- **Non-smooth or inaccessible gradients** — when the function is defined by a closed-source tool, simulation, or experimental pipeline.
- **High-dimensional problems with low effective dimension** — PySTARS can focus search in low-dimensional subspaces to improve efficiency.

If accurate, inexpensive gradients are available, a derivative-based method (such as those in SciPy) is generally a better choice.

---

## Details of the PySTARS Algorithm

PySTARS is a **trust-region method** that operates in a low-dimensional random subspace of the full variable space.  
Given a current iterate \(x_k\):

1. **Subspace selection**: Choose a \(p\)-dimensional subspace \(Q_k\) (\(p \ll n\)) using one of several generator types (identity, Haar, scaled Haar, hashing-based).
2. **Interpolation set**: Sample points around \(x_k\) within the trust-region radius \(\delta_k\) to maintain a well-spaced geometry.
3. **Model construction**: Fit a quadratic model \(m_k(s)\) in the subspace using either a **Diagonal Hessian** or **Frobenius** model.
4. **Step computation**: Solve the trust-region subproblem in the subspace to find a trial step \(s_k\).
5. **Acceptance test**: Evaluate \(f(x_k + Q_k s_k)\) and compute the ratio of actual to predicted reduction.
6. **Trust-region update**:  
   - If the step is successful, accept it and possibly expand \(\delta_k\).  
   - If not, reject it and shrink \(\delta_k\).
7. **Adaptive subspace** (optional): Increase \(p\) when repeated failures occur, while reusing previous sample points.

In **stochastic mode**, function evaluations are replaced by Monte Carlo averages to reduce noise effects, and the same acceptance logic is applied.

Bound constraints are handled directly in the step computation to ensure feasibility.

---

## References

- A. R. Conn, K. Scheinberg, L. N. Vicente, *Introduction to Derivative-Free Optimization*, SIAM, 2009.  
- Original STARS methodology and random subspace trust-region approaches from derivative-free optimization literature.  
- PySTARS: implementation of a **stochastic trust-region method in random subspaces** with diagonal-Hessian and Frobenius models.