# Theory-Agnostic Nonclassicality Certification in an Integrated Photonics Circuit

This repository contains the Jupyter notebook and experimental data accompanying the paper *"Theory-agnostic nonclassicality certification in an integrated photonics circuit"* [arXiv:2609.18671 [quant-ph]](https://arxiv.org/abs/2609.18671). It includes all code and data needed to reproduce the numerical results presented in the paper.

## Overview

The notebook (`Nonclassicality-chip.ipynb`) certifies nonclassicality in a photonic prepare-and-measure experiment without assuming quantum theory, using the framework of generalised non-contextuality in Generalised Probabilistic Theories (GPTs). The analysis is organised into three parts:

1. **Nonclassicality certification (linear program).** Defines the simplex-embedding linear program that tests whether an accessible GPT fragment admits a non-contextual ontological model, and, if not, quantifies the robustness of contextuality `r`. Introduced in [Phys. Rev. Lett. 132, 050202 (2024)](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.132.050202) and adapted from [SimplexEmbeddingGPT-v2](https://github.com/RossiVinicius/SimplexEmbeddingGPT-v2).

2. **Theory-agnostic tomography.** Reconstructs a low-rank state/effect decomposition `D ≈ Sᵀ·E` of the experimental frequency tables via a seesaw quadratic-program algorithm, following [Nat. Commun. 17, 2474 (2026)](https://www.nature.com/articles/s41467-026-69030-x) and adapted from [NonclassicalityTests](https://github.com/Albert-Aloy/NonclassicalityTests).

3. **Experiment-specific analysis.** Models the three-mode photonic interferometer (tritter) used in the experiment, fits and validates the theoretical transition-probability model against the measured data, performs rank analysis to select the optimal tomographic rank `k*`, evaluates the robustness of contextuality on the reconstructed data, and runs a sanity check with a classically dephased version of the circuit that should not exhibit any nonclassicality.

## Repository contents

```
.
├── Nonclassicality-chip.ipynb   # Main analysis notebook
├── data/
│   └── Figure X/
│        ├── table_X_n.txt   # n-th data-table for the specific poissonian sampling, n from 0 to 9
│        └── trainranks_X.npy  # Contains already the rank analysis for the 10 data tables in the folder
└── README.md
```

> Note: If your local file layout differs, update the `path` variables in the relevant notebook cells accordingly.

## Requirements

The notebook was developed and tested with **Python 3.11**. Main dependencies:

- `numpy`
- `scipy`
- `sympy`
- `matplotlib`
- `cvxpy`
- `cvxopt`
- `pycddlib`
- `mosek` (optional but recommended, see below)

Install with:

```bash
pip install numpy scipy sympy matplotlib cvxpy cvxopt pycddlib mosek
```

**Notes:**
- Installing `pycddlib` may require additional compilers (especially on Linux) or Python development headers if building from source. See the [pycddlib installation guide](https://pycddlib.readthedocs.io/en/latest/quickstart.html#installation) for details.
- The nonclassicality assessments solve a linear program using the `MOSEK` solver. MOSEK is proprietary and may require a license (free academic licenses are available). It is strongly recommended for numerical stability and speed; alternative free `cvxpy`-compatible solvers may work but reproducibility of the exact results is not guaranteed.

## Usage

1. Clone the repository and install the dependencies above.
2. Ensure the `data/` folder (containing `exp.txt` and the `table_sample_*.txt` files) is present alongside the notebook, or update the file paths in the notebook to match your setup.
3. Open and run `Nonclassicality-chip.ipynb` in Jupyter, running cells sequentially from top to bottom.

**Runtime warning:** the rank-analysis step (Section "Sampling noisy data and rank analysis") runs a seesaw optimisation across multiple ranks and resampled tables, and can take several minutes to complete depending on your machine. Adjust `convergence_tolerance` if needed. 

## Acknowledgements

We thank Albert Aloy for his support with the theory-agnostic tomography functions. Some functions in this repository are inspired by the work of Jonathan Gross, Stelios Sfakianakis, and Mathew Weiss, who we hereby acknowledge. V.P.R. acknowledges partial support by the Digital Horizon Europe project FoQaCiA, Foundations of quantum computational advantage, GA No. 101070558, funded by the European Union, NSERC (Canada), and UKRI (UK). This work is partially carried out under the IRA Programme, project no. FENG.02.01-IP.05-0006/23, financed by the FENG program 2021-2027, Priority FENG.02, Measure FENG.02.01., with the support of the FNP.

## License

**Code:** The code in this notebook is licensed under the MIT License. You are free to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of it, provided that the original copyright notice and this permission notice are included in all copies or substantial portions of the code. See the `LICENSE` file for the full license text.

**Data:** The experimental dataset (`data/exp.txt`) is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0). You are free to share and adapt the data for any purpose, provided that appropriate credit is given to the original contributors and the associated publication [arXiv:2609.18671 [quant-ph]](https://arxiv.org/abs/2609.18671) is cited. See [creativecommons.org/licenses/by/4.0](https://creativecommons.org/licenses/by/4.0/) for details.

## Citation

If you use this code or data, please cite the associated publication [arxiv handler].
