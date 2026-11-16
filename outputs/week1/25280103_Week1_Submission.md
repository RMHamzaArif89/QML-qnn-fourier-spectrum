# 25280103 - Week 1 Progress Review Submission

**Project:** Data Re-uploading and the Fourier Spectrum of QNNs  
**Student:** Rana Muhammad Hamza  
**Roll number:** 25280103  
**Course:** QML  
**Instructor:** Dr Faryad  
**Run date:** 2026-11-16  
**Kernel:** Project .venv, Python 3.11.9  
**Root seed:** 42

## What to submit for Week 1

1. This progress-review report, including the introduction, methods, results, and submission checklist.
2. The executed notebook: notebooks/week1_progress_review.ipynb.
3. The reproducibility bundle in outputs/week1: saved inputs and fixed folds, CSV tables, NPZ predictions and model parameters, figures, week1_run_config.json, and week1_results_summary.md.
4. The project README, requirements file, and code in the GitHub repository: https://github.com/RMHamzaArif89/QML-qnn-fourier-spectrum

The Week 1 schedule calls for the data pipeline, fixed folds, classical baselines, first quantum model, an introduction and methods report draft, and code on GitHub. The report draft and runnable evidence are included below and in the notebook.

## Introduction

Quantum machine-learning models encode classical inputs into quantum states and use trainable operations to make predictions. Data re-uploading alternates input-dependent gates with trainable gates, allowing a compact circuit to build richer functions through repeated encoding. Prior work relates this encoding structure to the Fourier components available to variational quantum models (Pérez-Salinas et al., 2020; Schuld, Sweke, and Meyer, 2021).

This project asks how encoding repetitions and layer count shape the frequencies a quantum neural network can represent, and how the encoding layout affects that representation. For a feature encoded by L occurrences of Pauli rotations exp(-i x P / 2), the candidate integer harmonics are expected to lie within -L through L. These are possible frequencies; training does not guarantee that every allowed coefficient appears.

The Week 1 checkpoint establishes the seeded data pipeline and fixed classification folds, evaluates classical baselines, and compares one-qubit re-uploading regressors at L=1, 2, and 3. A reproducible coefficient outside the predicted frequency support would challenge the hypothesis only if it exceeds the predeclared threshold and persists on a refined grid and across initializations.

## Methods

### Synthetic regression

Inputs are sampled uniformly from [-pi, pi) using root seed 42. The 1D target is f1(x) = 0.5 cos(x) + 0.3 sin(2x) + 0.2 cos(3x), with 128 training samples and a separate 256-point evaluation grid. The 2D target is f2(x1, x2) = 0.4 sin(x1) + 0.3 cos(2x2) + 0.3 sin(x1 - x2), with 2,048 training samples and a separate 64 by 64 evaluation grid.

### Classification and folds

The balanced synthetic two-spiral dataset contains 1,000 examples per class. One shuffled, stratified five-fold split is created with seed 42. The fold indices are saved and reused for both classifiers. Any learned scaling is fit inside the training-fold estimator pipeline.

### Classical baselines

Regression uses Fourier-feature linear models with harmonics through K=3 and small MLPs. The 1D MLP has seven parameters, close to the six trainable angles in the L=3 QNN. The 2D Fourier model and 2D MLP each have 49 coefficients or parameters. Spiral classification compares Fourier-feature logistic regression through K=4 with an MLP classifier.

### First quantum model and spectrum check

The noiseless model is an exact NumPy statevector simulation of a one-qubit circuit. Each layer re-uploads x with an RY rotation and applies trainable RZ and RY rotations. L=1, 2, and 3 are evaluated with initialization seeds 0 through 4, full-batch Adam, learning rate 0.01, and at most 1,000 updates. Parameter-shift gradients are used. The trained outputs are evaluated on 256- and 512-point grids and transformed with a discrete Fourier transform. The threshold for an out-of-support coefficient is max(1e-6, 0.01 times the largest coefficient).

## Results

### Regression

| Task | Model | Parameters | Dense-grid MSE |
| --- | --- | ---: | ---: |
| 1D | Fourier linear, K <= 3 | 7 | 4.89e-32 |
| 1D | MLP 1-2-1 | 7 | 0.0268 |
| 1D | QNN L=1 | 2 | 0.065933 +/- 0.000000 |
| 1D | QNN L=2 | 4 | 0.164087 +/- 0.023762 |
| 1D | QNN L=3 | 6 | 0.016898 +/- 0.010670 |
| 2D | Fourier linear, |k_j| <= 3 | 49 | 3.30e-31 |
| 2D | MLP 2-12-1 | 49 | 9.58e-05 |

Across five QNN initializations, L=3 has the lowest mean dense-grid MSE. L=2 performs worse than L=1, showing that increased candidate frequency support alone does not ensure an improved fit.

### Fourier spectrum

The target third-harmonic amplitude is 0.200. Mean QNN amplitudes are 0.000000 +/- 0.000000 at L=1, 0.000000 +/- 0.000000 at L=2, and 0.119851 +/- 0.139311 at L=3. No above-threshold out-of-support coefficient was found in the 30 layer, seed, and grid checks. The L=3 circuit permits the third harmonic but does not consistently learn its full target amplitude.

### Spiral classification

| Model | Parameters | Accuracy, mean +/- SD | Macro F1, mean +/- SD |
| --- | ---: | ---: | ---: |
| Fourier logistic, K <= 4 | 81 | 0.9895 +/- 0.0041 | 0.9895 +/- 0.0041 |
| MLP 2-5-1 | 21 | 0.6230 +/- 0.0590 | 0.6212 +/- 0.0591 |

The Fourier logistic result is much higher on these fixed folds, but it uses 81 parameters compared with the MLP's 21, so the comparison is not capacity matched.

## Conclusion and limitations

The Week 1 pipeline, fixed-fold protocol, classical baselines, first QNN comparison, Fourier diagnostics, and introduction/methods draft are complete and reproducible. The MLP fits emitted convergence warnings at their configured iteration limits, so their results are provisional. The QNN results come from a noiseless statevector simulator; this checkpoint does not include a quantum spiral classifier, the L=4-6 sweep, 2D serial/parallel QNNs, noise sweeps, or hardware measurements. These are subsequent project milestones.

## Week 1 artifact index

- notebooks/week1_progress_review.ipynb - full pipeline, executed cells, report draft, and plots.
- outputs/week1/week1_results_summary.md - concise latest results.
- outputs/week1/week1_run_config.json - seed, package versions, folds, and model settings.
- outputs/week1/regression_baselines.csv and outputs/week1/spiral_classification_baselines.csv - classical baseline scores.
- outputs/week1/qnn_1d_initializations.csv, outputs/week1/qnn_1d_spectrum_check.csv, and outputs/week1/qnn_1d_third_harmonic_summary.csv - QNN fits and spectral diagnostics.
- outputs/week1/week1_inputs_and_fixed_folds.npz - generated data and fixed folds.
- Remaining CSV, NPZ, and PNG files in outputs/week1 contain per-fold scores, predictions, parameters, and figures.

## References

1. A. Pérez-Salinas et al., “Data re-uploading for a universal quantum classifier,” Quantum 4, 226 (2020), doi:10.22331/q-2020-02-06-226.
2. M. Schuld, R. Sweke, and J. J. Meyer, “Effect of data encoding on the expressive power of variational quantum-machine-learning models,” Physical Review A 103, 032430 (2021), doi:10.1103/PhysRevA.103.032430.
