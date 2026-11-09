# Data Re-uploading and the Fourier Spectrum of QNNs

**Project 9 · Course:** QML · **Student:** Rana Muhammad Hamza · **Roll number:** 25280103 · **Instructor:** Dr Faryad

## Project overview

This project investigates how data-encoding repetitions and circuit depth affect the frequencies a quantum neural network (QNN) can represent. It will fit periodic one- and two-dimensional target functions with one to six data re-uploading layers, analyze the trained models' Fourier spectra, compare serial and parallel feature encoding, and evaluate a small classification task.

## Initial synopsis

The two-column IEEE conference-style project synopsis, including the research question, falsifier, data, models, baselines, and milestone schedule, is in [`synopsis.tex`](synopsis.tex). Compile it with an IEEEtran LaTeX installation, for example:

```powershell
pdflatex synopsis.tex
pdflatex synopsis.tex
```

### Research question

How do encoding repetitions and layer count determine the frequencies a QNN can represent?

### Hypothesis and falsifier

For repeated Pauli rotations of the form `exp(-i x P / 2)` on a single feature, an encoding with `L` occurrences has candidate integer harmonics from `-L` to `L`. A reproducible Fourier coefficient outside that range in a noiseless simulation, above a predefined numerical tolerance and after ruling out sampling aliasing, would falsify this prediction for the circuit under study. Candidate frequencies are not necessarily all present: circuit structure and parameter values can suppress allowed modes.

## Research plan

1. **Synthetic regression:** fit periodic 1D and 2D target functions using one through six re-uploading layers. Analyze each model's spectrum on a uniform grid and report held-out error.
2. **Encoding comparison:** compare serial and parallel feature encoding. Record the encoding layout, trainable-parameter count, qubit count, circuit depth, and two-qubit gate count.
3. **Classical baselines:** compare against Fourier-feature linear regression and a small multilayer perceptron (MLP) with a matched parameter budget.
4. **Classification:** apply the models to Iris or a 2D spirals dataset, selecting and documenting the dataset, preprocessing, and evaluation protocol.
5. **Hardware evaluation:** run a trained one- or two-qubit model on IBM quantum hardware and compare its measured output with the simulator's fitted curve. Report the backend, shot count, and relevant circuit resources.

Use the course NB11 capstone starter harness for fixed folds, leakage-free preprocessing, classical baselines, ablations, and noise sweeps. Record random seeds and save the data and results needed to reproduce reported figures and tables.

## Setup

The current starter repository includes a Python environment-check notebook and `requirements.txt`. From the repository root, create and activate a virtual environment in PowerShell, then install the listed dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

In VS Code, install or enable the Python and Jupyter extensions, open [`notebooks/environment.ipynb`](notebooks/environment.ipynb), and select the project `.venv` as its kernel. Run the notebook cell to verify that the notebook is using that environment.

## Reproducing results

The current repository is an environment-setup starter; it does not yet include experiment scripts, trained models, saved results, or figure/table-generation commands. Therefore, no experimental results can be reproduced from this version yet. As the work is implemented, add the scripts or notebooks and exact commands here for each figure and table, along with the fixed random seeds, data-generation settings, preprocessing, and dependency versions. Save generated results in the repository so the report can be checked against them.

## Schedule and submissions

All groups present their progress, current report draft, and GitHub code every Sunday.

| Date (2026) | Weight | Milestone | What to submit or show |
| --- | ---: | --- | --- |
| Mon, Nov 2 | 0% | Project and group confirmed | Enter group names and the GitHub repository URL on the sign-up tab. |
| Sun, Nov 8 | 5% | Initial project synopsis | Submit a 1–2 page synopsis in the IEEE or APS LaTeX template. Include the research question, falsifier, data, models, baselines, and week-by-week plan. |
| Sun, Nov 15 | 15% | Week 1 progress review | Show the data pipeline, fixed folds, classical baselines, and first quantum model. Include the introduction and methods report draft, and code on GitHub. |
| Sun, Nov 22 | 25% | Week 2 progress review | Show full simulator results, the noise model, and ablations. Include a results-section draft and code on GitHub. |
| Sun, Nov 29 | 35% | Week 3 progress review and final presentations (first half of groups) | Have the IBM hardware result ready. Groups presenting on this date should bring the final talk. |
| Sun, Dec 6 | 20% | Final presentations (remaining groups) and final submission | All groups submit the final LaTeX report as a PDF and source, and tag a GitHub release. |

## Final deliverables

- **Report:** a two-column IEEE (IEEEtran) or APS (REVTeX 4.2) LaTeX report, suggested length 6–8 pages plus references. Include an abstract, introduction, background, methods, results, discussion, and conclusion. State the research question and falsifier; report resource counts (qubits, depth, two-qubit gates, and shots) and an author-contributions statement.
- **Presentation:** approximately 12 minutes plus 5 minutes for questions. Every group member presents a part.
- **Code on GitHub:** share the repository with the instructor. Include setup and figure/table reproduction instructions, a requirements file, fixed seeds, saved results, commits from every member, and a tagged final version.
- **Starter harness:** use NB11 for folds, leakage-free preprocessing, baselines, ablations, and noise sweeps.

## References

1. A. Pérez-Salinas et al., “Data re-uploading for a universal quantum classifier,” *Quantum* **4**, 226 (2020). [doi:10.22331/q-2020-02-06-226](https://doi.org/10.22331/q-2020-02-06-226)
2. M. Schuld, R. Sweke, and J. J. Meyer, “Effect of data encoding on the expressive power of variational quantum-machine-learning models,” *Physical Review A* **103**, 032430 (2021). [doi:10.1103/PhysRevA.103.032430](https://doi.org/10.1103/PhysRevA.103.032430)
