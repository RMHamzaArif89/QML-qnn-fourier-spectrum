# Week 1 Advancement Output Bundle

**Student:** Rana Muhammad Hamza
**Roll number:** 25280103
**Prepared:** 19 November 2026

This folder contains the reproducible extension of the Week 1 QML study and a separate execution of the course NB11 harness.

## Advancement experiment

- Notebook: `notebooks/25280103_Week1_Advancement_Task.ipynb`
- Data: the saved Week 1 NPZ input bundle; the original target plus a new known high-harmonic target at k=1, 4, and 6.
- Protocol: L=1-6, five initialization seeds, exact NumPy one-qubit statevector, RY/RX gate-axis ablation, parameter-shift gradients, 256/512-point spectra, and 20 finite-shot repeats at 128/512/2,048 shots.
- Main result: the six-layer high-harmonic RY model has 0.01002 +/- 0.00784 grid MSE; the paired RX ablation has 0.00277 +/- 0.00356. All 120 trained-model/grid support checks found zero above-threshold out-of-support modes.
- Outputs: layer-sweep and summary CSVs, gate-axis and finite-shot CSVs, resource counts, prediction archives, configuration, and four figures.
- Report: `report/Week1_Advancement_Report_25280103.pdf`.

## NB11 harness

- Notebook: `01_regression_and_spectra.ipynb`.
- Dataset: the harness's 120-example, six-feature, interaction-rich synthetic binary classification dataset; seed 0 and fixed stratified five-fold validation.
- Main result: ZZ kernel accuracy 0.700 +/- 0.096; tuned RBF SVM accuracy 0.892 +/- 0.042; shuffled-label leakage check passed.
- Outputs: classification folds, depolarizing and finite-shot summaries, circuit resources, configuration, and two figures in `nb11/`.
- Report: `report/NB11_Capstone_Report_25280103.pdf`.

All reported quantum measurements are simulator results. No hardware execution is included.
