# Five ML Algorithms from Scratch

**[`ml_algorithms_from_scratch.ipynb`](ml_algorithms_from_scratch.ipynb)** — linear
regression, logistic regression, PCA, a one-hidden-layer neural network with
backpropagation, and a dual-form SVM solved by SMO. Written with plain NumPy: no
scikit-learn, no PyTorch, no autograd.

scikit-learn is used for two things only — loading the datasets, and checking that the
answers are right.

Each section follows the same four steps: the idea, the code, the check against
scikit-learn, and a plot. The notebook is saved with its outputs, so it reads on GitHub
without being run.

**18 / 18 checks pass.**

| Check | Mine | Reference |
|---|---|---|
| Linear regression coefficients | `1.38e-12` | `LinearRegression` |
| Ridge coefficients | `5.33e-13` | `Ridge` |
| Gradient descent vs direct solve | `1.91e-07` | same problem, two methods |
| Logistic regression coefficients (Newton) | `7.65e-07` | `LogisticRegression` |
| PCA variance ratios and components | `0.00e+00` | `PCA` |
| PCA components orthonormal | `2.22e-15` | — |
| My gradients vs measured slopes | `3.86e-09` | finite differences |
| Neural net on digits | 0.9778 | 0.9733 (`MLPClassifier`) |
| SVM (RBF) accuracy · support vectors | 0.958 · 102 | 0.958 · 102 (`SVC`) |
| SVM boundary agreement | `1.0000` | correlation with `SVC` |
| SVM constraint Σαᵢyᵢ = 0 | `7.01e-08` | relative to Σα |

## Notes on the code

The implementations are deliberately plain — small functions, no class hierarchies, no
framework-style abstractions.

- The network uses four named arrays (`W1, b1, W2, b2`) instead of a general list of
  layers, and trains with ordinary mini-batch gradient descent.
- The SVM uses the simplified version of SMO, where the second multiplier is picked at
  random rather than by a heuristic. It is shorter to read and finds the same boundary;
  the trade-off is a few extra small non-zero multipliers.
- Both PCA routes are included — via SVD and via eigenvectors of the covariance matrix —
  and checked against each other.

## What the plots show

- Gradient descent converging onto the answer the direct solve already found.
- Ridge coefficient paths as the penalty grows.
- Newton's method settling in 8 steps where gradient descent needs thousands.
- PCA reconstructions of a digit from 5, 20 and 40 components.
- Gradient-check error against step size — too large is inaccurate, too small is noisy.
- SVM margins and support vectors for a straight and an RBF boundary, and what `C` does.

## Project page

`index.html` is a GitHub Pages project page for this repo. Enable Pages on the repository
(Settings → Pages → deploy from the `main` branch, root folder) and it renders at
`https://<username>.github.io/ml-from-scratch/`. It pulls its figures from `assets/`,
which are exported straight out of the notebook, so the page and the notebook cannot
drift apart.

## Running it

```bash
pip install -r requirements.txt
jupyter notebook ml_algorithms_from_scratch.ipynb
```

Runs end to end in under a minute on a laptop CPU.
