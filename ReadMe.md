# SINDy ODE Discovery Project

Overview
--------
This repository demonstrates discovery of ordinary differential equations (ODEs)
from trajectory data using the SINDy (Sparse Identification of Nonlinear Dynamics)
approach. The main work is performed in the Jupyter notebook `SindY.ipynb` and the
trajectory data is stored in `ODE.npy`.

Files
-----
- `ODE.npy` — NumPy array containing trajectory data with shape (m, N, n).
- `SindY.ipynb` — Notebook that loads the data, performs smoothing/derivative
	estimation, builds a polynomial library, fits SINDy (Lasso or least-squares),
	and evaluates / simulates the learned dynamics (including basin plots).
- `Xi_learned.npy`, `Xi_learned_lstsq.npy` — coefficient matrices saved by the
	notebook after fitting (if you run the notebook cells that save them).

Requirements
------------
- Python 3.8+ (tested with 3.9+)
- numpy
- scipy
- scikit-learn
- matplotlib

You can install the primary dependencies with:

```bash
python -m pip install numpy scipy scikit-learn matplotlib
```

Quick start
-----------
1. Open `SindY.ipynb` in Jupyter Lab / Notebook.
2. Ensure `ODE.npy` is in the same folder as the notebook (it is by default).
3. Run the cells in order. Key sections are:
	 - Data loading and visualization
	 - Smoothing and derivative estimation (Savitzky–Golay)
	 - Building the feature library (polynomial terms, optional sines)
	 - Fitting SINDy (Lasso or least-squares variants provided)
	 - Simulation / RK4 rollout and basin-of-attraction visualization

Reproducing results
-------------------
- Set a deterministic seed where indicated in the notebook (the code uses
	NumPy RNG seeds in several places).
- Tune smoothing (`window_length`, `polyorder`) and library `poly_order` to
	influence model complexity and stability of learned dynamics.
- For sparse discovery, run the Lasso-based `fit_sindy` variant and adjust
	`alpha` to control sparsity.

Notes and tips
--------------
- The notebook provides two fitting routes: a Lasso-based sparse fit and a
	least-squares fit. Use Lasso to encourage sparsity in `Xi`.
- Smoothing / derivative estimation is crucial for noisy data. Adjust the
	Savitzky–Golay window length and polynomial order accordingly.
- Simulation uses an RK4 integrator with optional substeps; reduce the
	simulation timestep (`dt_sim`) if trajectories diverge.

Outputs
-------
- Learned coefficient matrices are saved as `.npy` files by the notebook.
- Plots (phase portraits, prediction vs ground truth, basin maps) are shown
	inline in the notebook.

Next steps
----------
- If you'd like, I can add a `requirements.txt`, create a small script to run
	the pipeline non-interactively, or add example commands to reproduce the
	saved models from scratch.

License & Contact
-----------------
This repo contains analysis code and data for exploration. If you want me to
add a license or author/contact info, tell me how you want it formatted.

