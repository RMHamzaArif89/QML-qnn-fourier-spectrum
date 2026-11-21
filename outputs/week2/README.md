# Week 2 Simulator Results Bundle

**Student:** Rana Muhammad Hamza  
**Roll number:** 25280103  
**Milestone:** Week 2, full simulator results / noise / ablations

## Notebook

Run `notebooks/25280103_Week2_Simulator_Results.ipynb` from the project root with the **Python (QNN Fourier Spectrum)** kernel. It reads the saved Week 1 data and fixed folds, reuses the completed Week 1 Advancement 1D sweep, and writes all Week 2 outputs into this folder.

## Experiment coverage

- 2D periodic regression, serial one-qubit and parallel two-qubit encoding, L=1-6, five paired seeds, 1,000 full-batch Adam updates per fit.
- DFT support checks on 64x64 and refined 128x128 grids using `max(1e-6, 0.01*c_max)`.
- L=3 depth control with exactly three feature encodings and six trainable parameters; CNOT removal ablation.
- Two-spiral classification with the saved five folds, a Fourier logistic model, a five-parameter MLP, and a two-qubit re-uploading QNN.
- Qiskit Aer depolarizing noise after one-qubit rotations and CNOTs, with 1,024 shots per point and five repeats at four noise rates.

## Files

- `week2_2d_layer_sweep.csv`, `week2_2d_layer_summary.csv`, `week2_2d_spectrum_support.csv`
- `week2_2d_ablations.csv`, `week2_2d_ablation_summary.csv`, `week2_circuit_resources.csv`
- `week2_spiral_classification_fold_scores.csv`, `week2_spiral_classification_summary.csv`
- `week2_depolarizing_finite_shot_repeats.csv`, `week2_depolarizing_finite_shot_summary.csv`
- `week2_run_config.json`, trained parameters and prediction NPZ files, `figures/`
- Results draft: `report/Week2_Results_Draft_25280103.pdf`

All quantum data in this bundle comes from statevector or Qiskit Aer simulation. The hardware evaluation is scheduled for Week 3.
