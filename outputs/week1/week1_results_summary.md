# Week 1 results summary

**Student:** Rana Muhammad Hamza  
**Roll number:** 25280103  
**Course:** QML  
**Latest run:** 2026-11-16 in VS Code using the project .venv kernel (Python 3.11.9). Root seed: 42. Package versions and run settings are recorded in week1_run_config.json.

## Data and protocol

- 1D regression: 128 seeded training samples and a separate 256-point dense grid over [-pi, pi).
- 2D regression: 2,048 seeded training samples and a separate 64 by 64 evaluation grid.
- Spiral classification: 1,000 examples per class and one fixed, stratified five-fold split. The same saved folds are used for both baselines.
- QNN: exact NumPy one-qubit statevector simulation; L=1, 2, and 3; five initialization seeds; 2, 4, and 6 trainable angles; full-batch Adam at learning rate 0.01 for up to 1,000 updates.
- Spectrum: DFT checks at 256 and 512 points using the predeclared threshold max(1e-6, 0.01 times the largest coefficient).

## Dense-grid regression MSE

| Task | Model | Parameters | Dense-grid MSE |
| --- | --- | ---: | ---: |
| 1D | Fourier linear, K <= 3 | 7 | 4.89e-32 |
| 1D | MLP 1-2-1 | 7 | 0.0268 |
| 1D | QNN L=1 | 2 | 0.065933 +/- 0.000000 (5 seeds) |
| 1D | QNN L=2 | 4 | 0.164087 +/- 0.023762 (5 seeds) |
| 1D | QNN L=3 | 6 | 0.016898 +/- 0.010670 (5 seeds) |
| 2D | Fourier linear, |k_j| <= 3 | 49 | 3.30e-31 |
| 2D | MLP 2-12-1 | 49 | 9.58e-05 |

The Fourier regression baselines recover the known targets to numerical precision. L=3 has the lowest mean QNN error in this run; L=2 is worse than L=1, so greater candidate frequency support did not guarantee a better fit.

## Spectrum and third harmonic

The target third-harmonic amplitude 2|c3| is 0.200. The measured QNN mean +/- standard deviation is:

| Layers | QNN amplitude | Absolute error from target |
| ---: | ---: | ---: |
| 1 | 0.000000 +/- 0.000000 | 0.200000 |
| 2 | 0.000000 +/- 0.000000 | 0.200000 |
| 3 | 0.119851 +/- 0.139311 | 0.131435 |

No above-threshold out-of-support modes were found in 30 layer, seed, and grid checks. L=1 and L=2 cannot represent the target third harmonic under this encoding. L=3 permits it, but the learned mean remains below the target with substantial seed-to-seed spread.

## Spiral classification baselines

| Model | Parameters | Accuracy, mean +/- SD | Macro F1, mean +/- SD |
| --- | ---: | ---: | ---: |
| Fourier logistic, K <= 4 | 81 | 0.9895 +/- 0.0041 | 0.9895 +/- 0.0041 |
| MLP 2-5-1 | 21 | 0.6230 +/- 0.0590 | 0.6212 +/- 0.0591 |

The Fourier logistic classifier has 81 parameters versus 21 for the MLP, so this is not a matched-capacity comparison.

## Limitations

- The regression MLP and spiral MLP emitted convergence warnings at their configured iteration limits; treat those MLP results as provisional.
- The QNN is a noiseless NumPy statevector simulation. There is no quantum spiral classifier, 2D serial/parallel QNN comparison, noise sweep, gate-resource study, or hardware result in this Week 1 run.
- This checkpoint covers L=1, 2, and 3 only. The L=4-6 sweep and remaining simulator/hardware work are later milestones.

## Output files

The CSV and NPZ files in this folder store per-seed results, fixed folds, generated inputs, predictions, parameters, and spectrum checks. Figures show the data, baseline fits, QNN layer comparison, and spectrum/third-harmonic comparison. The run configuration records the seed, package versions, and model settings.
