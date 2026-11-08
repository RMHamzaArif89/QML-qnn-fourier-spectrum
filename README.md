# Data Re-uploading and the Fourier Spectrum of QNNs

**Project 9 · Quantum Neural Networks · Rana Muhammad Hamza (Instructor)**

[Research plan](#research-plan) · [Notebook setup](#notebook-setup) · [Milestones](#milestones) · [Deliverables](#deliverables) · [References](#references)

## Research plan

**Question.** How do encoding repetitions and layer count determine the frequencies a quantum neural network can represent?

**Hypothesis and falsifier.** For repeated Pauli rotations of the form exp(−ixP/2) on a single feature, an encoding with L occurrences has candidate harmonics at integer frequencies from −L to L. A reproducible coefficient outside this range in noiseless simulation, above a predefined numerical tolerance and after ruling out sampling aliasing, would falsify the prediction for that circuit. Compare candidate frequencies with measured coefficients because circuit structure and parameters can suppress allowed modes.

1. Fit synthetic 1D and 2D periodic functions with one to six re-uploading layers. Use noiseless Fourier analysis on a uniform grid and report held-out error alongside the spectra.
2. Compare serial and parallel encoding. Record feature encodings, trainable parameters, qubits, depth and two-qubit gates so comparisons show how resources differ.
3. Benchmark against Fourier-feature linear regression and a small MLP with a matched parameter budget. Use fixed seeds and the course NB11 harness for folds, leakage-free preprocessing, baselines, ablations and noise sweeps.
4. Run a small classification experiment using Iris or 2D spirals. Compare simulator results with an IBM hardware run for a trained one- or two-qubit model and report shot counts alongside the fitted curve.

## Notebook setup

Open the repository in VS Code with the Python and Jupyter extensions. On Windows, create and activate the environment in a PowerShell terminal from the repository root.

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

The terminal prompt should start with `(.venv)`. Open [the environment check notebook](notebooks/00_environment.ipynb) and select **Python Environments → .venv** in the kernel picker. The notebook checks which Python executable the kernel is using.

<details>
<summary>What is included in this initial repository?</summary>

The notebook checks the Python environment. The experiments, NB11 integration, results, and report are planned milestones. Figure and table reproduction commands will be added as results are generated.

</details>

## Milestones

| Date (2026) | Weight | Review or submission |
| --- | ---: | --- |
| Nov 2 | 0% | Confirm group and project. Enter names and GitHub URL in the sign-up tab. |
| Nov 8 | 5% | Submit a 1–2 page IEEE or APS synopsis with the question, falsifier, data, models, baselines, and weekly plan. |
| Nov 15 | 15% | Show data pipeline, fixed folds, baselines, and first QNN. Draft introduction and methods. |
| Nov 22 | 25% | Show simulator results, noise model, and ablations. Draft results. |
| Nov 29 | 35% | Show IBM hardware results. First half of groups present. |
| Dec 6 | 20% | Remaining groups present. Submit report PDF and LaTeX source and tag the final GitHub release. |

Bring the current report draft and GitHub code to each Sunday review.

## Deliverables

- [ ] IEEEtran or REVTeX 4.2 report, suggested 6–8 pages plus references. Include abstract, introduction, background, methods, results, discussion, conclusion, falsifier, resource counts, and author contributions.
- [ ] Group presentation, suggested 12 minutes plus 5 minutes for questions. Every member presents.
- [ ] GitHub repository shared with the instructor, with commits from every member, requirements, fixed seeds, saved results, reproduction instructions for each figure and table, and a tagged final release.

## References

1. A. Pérez-Salinas et al., “Data re-uploading for a universal quantum classifier,” *Quantum* **4**, 226 (2020). [DOI](https://doi.org/10.22331/q-2020-02-06-226)
2. M. Schuld, R. Sweke, and J. J. Meyer, “Effect of data encoding on the expressive power of variational quantum-machine-learning models,” *Phys. Rev. A* **103**, 032430 (2021). [DOI](https://doi.org/10.1103/PhysRevA.103.032430)
