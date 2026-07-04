# Noncommutative Interpolatory Subdivision on the Heisenberg Group


> **A Heisenberg Subdivision Scheme with Central Smoothness Loss**
> H. Ugail and A. Carriazo

Subdivision schemes build a smooth curve from a coarse control polygon by repeatedly inserting new points according to a fixed local rule. In ordinary Euclidean space the four-point scheme of Dyn, Gregory and Levin is a classic example, and its limit curve is continuously differentiable. A natural question is what happens when the data no longer live in flat space but in a curved or noncommutative geometry, where the coordinates interact through a group law rather than adding independently.

In this project, we study that question in the simplest noncommutative setting, the three-dimensional Heisenberg group. The horizontal coordinates are refined exactly as in the Euclidean four-point scheme, and the third, central coordinate is corrected by a term dictated by the group law. The correction is small, geometrically natural, and harmless at any single refinement step.

The surprise is that this natural correction affects smoothness. The horizontal part of the limit curve stays continuously differentiable, but the central part does not. It remains continuous, and in fact sits in the Zygmund class, yet it fails to be continuously differentiable because the correction feeds in a signal that never decays as refinement proceeds. The notebook in this repository makes the effect visible and measurable, showing the central coordinate lifting away from flat data, its sensitivity to the order in which points are visited, its convergence rate, and the linear growth that witnesses the loss of a derivative.

The wider point is a cautionary one for anyone designing subdivision or refinement rules on groups and manifolds. Compatibility with the group law does not by itself guarantee a smooth limit.


## Technical details

The scheme refines a control polygon whose vertices live in the three-dimensional
Heisenberg group. The two horizontal coordinates `(x, y)` are refined by the
classical four-point interpolatory mask of Dyn, Gregory and Levin, and the central
coordinate `z` receives a closed-form correction read off the group law,

```
R_i = (1/2) ( x_i * b_i  -  y_i * a_i ),   a_i = X - x_i,   b_i = Y - y_i,
```

where `(X, Y)` are the horizontally refined values at the inserted point.

The central finding is a negative regularity result. The horizontal limit is
exactly the classical four-point limit and is `C^1`. The central limit is
continuous and belongs to the Zygmund class, but it is **not** `C^1`. The scaled
correction converges to a nonzero limit, `2^k R_i -> (1/4)(X Y' - Y X')`, so the
forcing injected at every refinement level does not decay. As a result the scaled
central first differences grow linearly in the refinement level, while the second
differences stay bounded.

## What the notebook produces

| Figure | File | Content |
|--------|------|---------|
| 1 | `fig1_lifting.png` | Central-coordinate lifting from flat (L-shaped) data |
| 2 | `fig2_order.png` | Order sensitivity of the central coordinate |
| 3 | `fig3_C0_convergence.png` | Uniform `C^0` convergence at rate `O(2^-k)` |
| 4 | `fig4_non_C1_witness.png` | Linear growth of scaled first differences and the bounded Zygmund quotient |

Each figure is exported as a 300 dpi PNG. The notebook also prints a convergence
table and a numerical check that the limiting correction coefficient is `1/4`.

## Requirements

The notebook depends only on the standard scientific Python stack. Tested with
Python 3.10 and later.

```
numpy
matplotlib
pandas
jupyter
```

Install them with

```bash
pip install -r requirements.txt
```

## Running

Open the notebook and run all cells,

```bash
jupyter notebook heisenberg_subdivision_numerics.ipynb
```

or execute it non-interactively from the command line,

```bash
jupyter nbconvert --to notebook --execute heisenberg_subdivision_numerics.ipynb
```

Running all cells regenerates the four figures in the working directory.

## Repository contents

```
heisenberg_subdivision_numerics.ipynb   the experiments and figures
requirements.txt                        Python dependencies
LICENSE                                 MIT licence
.gitignore                              standard Python and Jupyter ignores
README.md                               this file
```

## Reproducibility notes

- The four-point parameter is fixed at `omega = 1/16` throughout.
- Examples 1 to 3 use the open scheme with index clamping at the two endpoints.
- The forcing and Zygmund diagnostics use a periodic scheme so that boundary
  effects do not contaminate the interior measurements.
- All randomness is absent; every result is deterministic given the control
  polygons defined in the notebook.

## Citation

If you use the cross-replay paradigm, the code in this repository, or the precomputed result tables, please cite:

> H. Ugail, A. Carriazo, *A Heisenberg Subdivision Scheme with Central Smoothness Loss*, 2026, Under review.

## License

Released under the MIT License. See [`LICENSE`](LICENSE) for details.
