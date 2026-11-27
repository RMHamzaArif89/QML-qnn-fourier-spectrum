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
python -m venv .venv-qml
.\.venv-qml\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m ipykernel install --user --name qnn-fourier-spectrum --display-name 'Python (QNN Fourier Spectrum)'
```

In VS Code, install or enable the Python and Jupyter extensions, open [`notebooks/environment.ipynb`](notebooks/environment.ipynb), and select the **Python (QNN Fourier Spectrum)** kernel (`qnn-fourier-spectrum`). The workspace is configured to use `.venv-qml`; run the environment notebook cell to verify the selected interpreter and installed packages. The requirements include Qiskit and Qiskit Aer for NB11, along with the scientific Python and notebook execution packages.

## Reproducing results

The Week 1 implementation is [`notebooks/week1_progress_review.ipynb`](notebooks/week1_progress_review.ipynb). Open it from the project root in VS Code, select the **Python (QNN Fourier Spectrum)** kernel (`qnn-fourier-spectrum`), and run all cells. Its first code cell checks for NumPy, pandas, Matplotlib, IPython, and scikit-learn; if any are missing, it installs the project requirements into the selected kernel before importing them. Package installation requires access to the configured package index. The notebook records the seed and package versions, creates the seeded 1D and 2D regression data, generates the balanced spiral dataset and fixed stratified folds, evaluates the classical baselines, and trains one-qubit regressors at L=1, 2, and 3.

Generated Week 1 inputs, folds, predictions, parameters, summaries, spectrum diagnostics, and figures are saved under `outputs/week1/`; see `outputs/week1/week1_results_summary.md` for the baseline interpretation. The Week 1 baseline notebook covers L=1-3. The advancement notebook extends the one-qubit study through L=6, adds a high-harmonic target, compares RY/RX data gates with paired initializations, tests Fourier support at 256- and 512-point grids, and evaluates finite-shot sampling. Its results, figures, configuration, and run index are in `outputs/week1Advancement/`.

## Week 1 advancement and NB11 evaluation

- Advancement notebook: [`notebooks/25280103_Week1_Advancement_Task.ipynb`](notebooks/25280103_Week1_Advancement_Task.ipynb). Run all cells with the QNN Fourier Spectrum kernel. It loads the saved Week 1 input NPZ file and writes its layer sweep, gate-axis ablation, spectra, shot study, resource counts, and figures under `outputs/week1Advancement/`.
- NB11 harness: [`01_regression_and_spectra.ipynb`](01_regression_and_spectra.ipynb). Run all cells with the same kernel. It records the preregistered question, fixed-fold baselines, Qiskit Aer shot-based ZZ kernel, leakage and ansatz checks, noise and finite-shot studies, and resource counts. Machine-readable outputs and figures are saved under `outputs/week1Advancement/nb11/`.
- Reports: [`report/Week1_Advancement_Report_25280103.pdf`](report/Week1_Advancement_Report_25280103.pdf) and [`report/NB11_Capstone_Report_25280103.pdf`](report/NB11_Capstone_Report_25280103.pdf).
- The Week 1 advancement and NB11 runs use simulator data only; neither report claims a hardware execution.

## Week 2 simulator results

- Notebook: [notebooks/25280103_Week2_Simulator_Results.ipynb](notebooks/25280103_Week2_Simulator_Results.ipynb). It reuses the completed Week 1 1D results and runs the 2D serial/parallel layer sweep, Fourier support checks, depth and CNOT ablations, spiral classification, and Aer depolarizing-noise study.
- Reproducible tables, trained parameters, run configuration, and figures: [outputs/week2/](outputs/week2/). See [outputs/week2/README.md](outputs/week2/README.md) for the bundle contents.
- Results draft: [report/Week2_Results_Draft_25280103.pdf](report/Week2_Results_Draft_25280103.pdf) and [report/Week2_Results_Draft_25280103.md](report/Week2_Results_Draft_25280103.md).
- Submission archive: [submission/25280103_Week2_Submission.zip](submission/25280103_Week2_Submission.zip); package guide: [submission/README_Week2_Submission_25280103.md](submission/README_Week2_Submission_25280103.md).
- The Week 2 study uses statevector and Qiskit Aer simulation; hardware evaluation is planned for Week 3.

## Week 3 IBM hardware evaluation

- Primary executable notebook: [notebooks/25280103_Week3_IBM_Hardware_Evaluation.ipynb](notebooks/25280103_Week3_IBM_Hardware_Evaluation.ipynb). It freezes the selected Week 1 one-qubit L=3 model (seed 3), compares exact and 1,024-shot Aer predictions, and records an IBM Runtime hardware execution. The notebook does not contain credentials.
- Hardware result bundle: [outputs/week3/](outputs/week3/). It contains the raw measurement counts, sampled predictions, error table, transpilation resources, backend and job metadata, figures, and run configuration. The completed IBM Runtime job ran on `ibm_marrakesh` with 64 circuits x 1,024 shots (65,536 total shots).
- Week 3 report: [report/Week3_IBM_Hardware_Evaluation_Report_25280103.pdf](report/Week3_IBM_Hardware_Evaluation_Report_25280103.pdf) and [report/Week3_IBM_Hardware_Evaluation_Report_25280103.md](report/Week3_IBM_Hardware_Evaluation_Report_25280103.md).
- The hardware result is scoped as a time-specific evaluation of one frozen QNN, not as a quantum-advantage claim.

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
