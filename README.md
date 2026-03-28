# L2 Regularization ≡ Virtual Samples

> **Interactive 3D visualization** showing that Ridge regression is equivalent to OLS with virtual training samples at the origin.

## [▶ Launch App](https://eopchang.github.io/l2-virtual-samples/)

---

## Core Idea

Ridge regression adds a penalty term λ‖**w**‖² to the OLS cost function. This is mathematically **identical** to adding *virtual data points* with target y = 0 and then running ordinary least squares on the augmented dataset:

```math
J(\mathbf{w}) = \underbrace{\lVert \mathbf{y} - \mathbf{X}\mathbf{w} \rVert^2}_{n \text{ real samples}} + \underbrace{\lVert \mathbf{0} - \sqrt{\lambda}\,\mathbf{I}\,\mathbf{w} \rVert^2}_{p \text{ virtual samples}}
```

where

```math
\mathbf{X} \in \mathbb{R}^{n \times p},\quad \mathbf{y} \in \mathbb{R}^{n},\quad \mathbf{w} \in \mathbb{R}^{p},\quad \sqrt{\lambda}\,\mathbf{I} \in \mathbb{R}^{p \times p}
```

The second term is the cost from **p virtual samples**: each sample $\mathbf{x}_v^{(j)} = \sqrt{\lambda}\,\mathbf{e}_j$ with $y_v = 0$ pulls the j-th weight toward zero — the hallmark of L2 regularization.

## Features

### p = 1 Mode (Single Feature)
- **Data Space** (left): regression line with the virtual sample (√λ, 0) visible as a blue diamond
- **Cost Landscape** (right): data cost + penalty cost curves, showing how the Ridge minimum shifts from OLS
- Add/remove data points, adjust λ in real time

### p = 2 Mode (Two Features, 3D)
- **3D Scene** (left): interactive Three.js view — rotate and zoom to see OLS/Ridge regression **planes** and data points in (x₁, x₂, y) space
- **Weight Space** (right): contour plot of J(w₁, w₂) with L2 constraint circle and OLS→Ridge path
- **Partial regularization**: choose 0, 1, or 2 virtual samples to regularize individual weight dimensions independently

### Controls
| Control | Function |
|---------|----------|
| **λ slider** | Regularization strength (0–10) |
| **Virtual Samples (0/1/2)** | Number of virtual samples — 0 = no penalty, 1 = partial L2, 2 = full L2 |
| **OLS / Ridge toggles** | Show/hide each model |
| **Presets** | Simple, Overfit, Noisy (p=1) · Simple, Collinear, Overfit (p=2) |
| **+ Random** | Add a random data point |

## Why This Matters: Cerebellar Learning

This visualization is motivated by computational neuroscience research on how the **cerebellum** might implement regularization:

- Cerebellar **parallel fibers (PFs)** are extremely numerous (~10⁸) but sparsely active
- Each PF can be viewed as a high-dimensional basis function with sparse activation → resembling a virtual sample anchored near zero
- The sparse PF activity pattern effectively implements **L2-like regularization** on Purkinje cell synaptic weights
- This may explain the cerebellum's remarkable ability to generalize motor control from limited training

## Tech Stack

- **Three.js** — 3D regression plane rendering with orbit controls
- **KaTeX** — LaTeX equation rendering
- **Vanilla JS** — No build step, single `index.html`

## Local Development

```bash
# Any static server works
npx serve .
# or
python3 -m http.server 3456
```

Then open `http://localhost:3456`.

> **Note:** Opening `index.html` directly via `file://` will fail due to ES module CORS restrictions. A local HTTP server is required.

## References

- Kim CE. *The Geometry of Generalization: Cerebellar Regularization via Sparse Virtual Samples* (2025)
- Theoretical Neuroscience & Computational Medicine Lab, Gachon University

## License

MIT
