[README.md](https://github.com/user-attachments/files/34471459/README.md)
# Patch-Based Neural Networks for Learning Derivatives and Solving PDEs in 2-D and 3-D

Python code for the paper by B. Shiri, D. Baleanu, Z. Alijani and J. J. Nieto.

Derivative stencils are learned from data by a linear patch-based network whose
weights are obtained by solving the normal equations (no gradient descent).
The learned stencils are then used in a marching solver for first-order PDEs.

## Installation

```
pip install -r requirements.txt
```

## Scripts

| Script | Paper section | Output |
|---|---|---|
| `train_2d_stencil.py` | Sections 2-3 | Table 2 (learned 2x2 stencils), Tables 3-4 (convergence tests) |
| `solve_pde_2d.py` | Section 4 | Example 1 (Fig. 1), Example 2 (Table 6, Fig. 2) |
| `two_layer_corrector.py` | Section 5 | Tables 7-8 (two-layer corrector) |
| `train_3d_stencil.py` | Section 6 | Table 9 (learned 2x2x2 stencils) |
| `solve_pde_3d.py` | Section 7 | Constrained 3D stencils, grid refinement, Figs. 3-4 |
| `common.py` | - | Shared routines: training sets, patches, training, marching solver |

Run any script from this folder, e.g.

```
python train_2d_stencil.py
```

Figures are saved in `results/`.

## Notes

- Arrays are indexed `F[i, j] = F(X_i, Y_j)`: the first array index is X.
- The linear systems are singular, so the learned weights are not unique.
  `numpy.linalg.lstsq` returns the minimum-norm solution; individual weights may
  therefore differ from those printed in the paper (computed with MATLAB's
  backslash), while the errors are of the same size.
