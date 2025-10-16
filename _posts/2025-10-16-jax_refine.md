---
layout: single
title: "Optimizing Molecular Dynamics Weights with Machine Learning Tools"
author: "James Holton, with contributions from Karson Chrispens, Steve, and Marcus Collins"
date: 2025-10-16
categories: 
	- posts
tags:
	- diffuse scattering
	- molecular dynamics
	- optimization
	- machine learning
excerpt: "Using gradient-based optimization to identify the most physically relevant portions of MD trajectories by maximizing agreement with diffuse scattering data."
---

In our latest round of diffuse scattering experiments, we ran into an intriguing optimization problem that feels a lot like training a neural network.

---

## The Scientific Setup

For each 3D pixel in reciprocal space (indexed by **h**), we have:

- **Observed data**, \(y(h)\) from experiment  
- **Predicted data**, \(x(h)\) computed from molecular dynamics (MD) trajectories  

We evaluate agreement using the **Pearson correlation coefficient**:

$$
\mathrm{CC} \;=\;
\frac{\langle x\cdot y\rangle - \langle x\rangle\langle y\rangle}
{\sqrt{\big(\langle x^2\rangle - \langle x\rangle^2\big)\,\big(\langle y^2\rangle - \langle y\rangle^2\big)}}
$$

Each prediction \(x(h)\) is derived from **structure factors** \(F(h, t)\) across time points in the MD simulation:

$$
x(h) \;=\; \langle F(h)^2\rangle_{t} \;-\; \langle F(h)\rangle_{t}^2
$$

The goal is to assign **weights** \(w(t)\) to each time point to maximize \(\mathrm{CC}\):

$$
x'(h) \;=\; \sum_{t} w_{t}\,F(h,t)^2 \;-\; \left(\sum_{t} w_{t}\,F(h,t)\right)^{2}
$$

If we can find optimal weights, we can identify which regions of the trajectory best match experimental reality — potentially distinguishing “good” frames from those that detract from agreement.

---

## Community Brainstorming

**Steve** suggested asking whether \(\mathrm{CC}\) is the right target — perhaps a likelihood might better capture the physics.

**Karson Chrispens** proposed leveraging machine learning frameworks like **JAX** or **PyTorch** to treat the weights as trainable parameters.  
By backpropagating through the Pearson correlation, an optimizer like Adam could efficiently learn the optimal weights.

**James Holton** suspected this approach could outperform traditional non-linear least-squares optimization and shared example MTZ datasets for testing.

**Steve** also mentioned using a **genetic algorithm** if the weights were binary (\(0\) or \(1\)), though he acknowledged the continuous formulation might not have a unique minimum.

---

## Prototyping the Optimizer

Karson quickly implemented a JAX-based prototype using **reciprocalspaceship** for MTZ I/O and **optax** for optimization.  
The loss function was simply \(-\mathrm{CC}\), and weights were constrained to \((0, 1)\) via a sigmoid transform.

When tested on toy datasets and real MTZ files, the optimizer:

- Successfully recovered **50:50** weights for mixtures of two “ground-truth” structures  
- Produced sensible intermediate values when one or both inputs were “wrong”  
- Converged robustly from different initializations  

Example output for a ground-truth mixture:

```

Final weights: [0.46, 0.54]
Final CC: 1.0000

```

And for mismatched data:

```

Final weights: [0.76, 0.24]
Final CC: 0.78

```

---

## Discussion

**Marcus Collins** noted that this approach resembles computing **Boltzmann-like factors** for each configuration and suggested PyTorch could be an equally good (and more common) platform.  
He also cautioned that Pearson \(\mathrm{CC}\) may not be the optimal objective function.

Karson confirmed that JAX runs efficiently on GPUs and planned to scale the approach to larger datasets by stacking multiple MTZ files.

---

## Where This Might Go Next

This prototype demonstrates that **gradient-based optimization** can efficiently identify the contribution of different MD frames to observed diffuse scattering patterns.  
Future directions include:

- Expanding to full MD trajectories with thousands of frames  
- Experimenting with alternate objectives (e.g., likelihood, cross-entropy)  
- Incorporating **crystal symmetry** and **resolution weighting**  
- Exploring physical interpretations of the resulting weights  

---

## Code and Data

Karson’s implementation, `pearson_target.py`, is available [here](https://github.com/k-chrispens/simulation_timeseries_optim), and the test MTZ data can be downloaded from  
[here](http://bl831.als.lbl.gov/~jamesh/pickup/diffUSE_CC_opt_test.tgz).

---

**TL;DR:**  
By treating MD frame weights as trainable parameters in a differentiable Pearson correlation objective, we can use ML optimizers like Adam to rapidly identify which parts of a trajectory best explain experimental diffuse scattering — turning a brute-force search into a smooth, data-driven optimization problem.

