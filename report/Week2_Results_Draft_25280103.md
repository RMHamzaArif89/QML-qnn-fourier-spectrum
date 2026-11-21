# Week 2 Results Draft
## Data Re-uploading and the Fourier Spectrum of QNNs
**Project 9 | Quantum Machine Learning**  
**Student:** Rana Muhammad Hamza | **Roll number:** 25280103  
**Report date:** 22 November 2026 | **Status:** Week 2 simulator results draft

## Executive summary
This report records the completed Week 2 simulator study: 1D Week 1 evidence reuse, 2D serial/parallel re-upload sweeps for L=1-6, two-grid Fourier support diagnostics, matched classical baselines, fixed-encoding depth and CNOT ablations, a five-fold two-spiral benchmark, and a Qiskit Aer depolarizing-noise/finite-shot experiment. It reports simulator results only; hardware evaluation is scheduled for Week 3.

The central result is that the parallel 2-qubit layout improves as L increases, reaching a mean 64x64 grid MSE of 0.0673 +/- 0.0061; the serial one-qubit layout reaches 0.1562 +/- 0.0259. No measured coefficient outside the declared coordinate-wise support crossed the preregistered threshold on either grid.

## 1. Introduction and research objectives
Data re-uploading repeats input-dependent rotations throughout a trainable quantum circuit. Fourier analysis connects those repeated encodings to the frequencies that the resulting model can express. Week 2 extends the Week 1 1D baseline with a controlled 2D study, then checks the findings in a small classification task and under a simulator noise model.

**Research question.** How do encoding repetitions and layer count set the frequencies a QNN can represent, and how do serial and parallel encodings affect fit quality and resources?

**Hypothesis.** Repeated Pauli-rotation encodings expand candidate Fourier support. The coordinate-wise frequency bound grows with the number of feature encodings. A two-qubit parallel circuit should learn the target mixed mode (1, -1) with improved regression as layers are added.

**Operational falsifier.** A measured coefficient outside the declared support must exceed max(1e-6, 0.01*c_max) and persist on both 64x64 and refined 128x128 grids. Results are summarized over five independent initializations.

**Objectives.** (1) Reuse the seeded Week 1 1D results; (2) fit the 2D target with L=1-6 and paired seeds; (3) compare serial and parallel encoding under equal 2L trainable parameters; (4) measure DFT support at two resolutions; (5) add depth and entanglement ablations; (6) compare Fourier, MLP, and QNN spiral classifiers on identical folds; and (7) quantify finite-shot depolarizing noise in Aer.

## 2. Dataset descriptions
- **1D synthetic regression:** the original Week 1 periodic target plus the Week 1 high-harmonic target; 128 fixed training inputs and a 256-point evaluation grid. The completed Week 1 Advancement sweep is reused directly.
- **2D periodic regression:** 2,048 fixed training points. The target is 0.4 sin(x1) + 0.3 cos(2x2) + 0.3 sin(x1-x2). Evaluation uses a 64x64 periodic grid and a refined 128x128 grid.
- **Two spirals:** 2,000 balanced synthetic examples (1,000 per class), using the same five saved stratified folds (1,600 train and 400 test observations per fold). The QNN inputs are scaled by pi; no test-fold statistic is used for preprocessing.

## 3. Methodology and experimental setup
The deterministic data bundle and folds are loaded from Week 1 with data seed 42. Regression uses Adam (learning rate 0.01), full-batch MSE, five initialization seeds (0-4), and at most 1,000 updates per fit. Gradients are computed with an exact statevector adjoint method and checked against central finite differences.

The **serial** circuit uses one qubit and applies RX(x1), RZ(x2), then two trainable rotations per re-upload layer. The **parallel** circuit uses two qubits, applies RX(x1) to q0 and RZ(x2) to q1, then a trainable pair and one CNOT per layer. Each has 2L unique trainable parameters. Counts are logical pre-transpilation resources.

Classical 2D references include a 49-coefficient Fourier-feature linear model (unique sine/cosine terms with |k_j|<=3) and a 49-parameter 2-12-1 MLP. The spiral baselines are an 81-feature Fourier logistic model (|k_j|<=4) and a five-parameter 2-1-1 MLP; the QNN has six trainable parameters and three parallel re-upload layers.

For spectrum checks, the 2D DFT is normalized and active coefficients are assessed against max(1e-6, 0.01*c_max), separately at 64x64 and 128x128. The noise model applies depolarizing channels after RX/RY/RZ and CX gates at p=0, 0.001, 0.005, and 0.01. It uses 1,024 shots for each of 256 deterministic points and five repeats per layout/rate. Even p=0 includes finite-shot sampling.

## 4. Results
### 4.1 Reused 1D Week 1 evidence
| Target | L | Parameters | Grid MSE mean +/- SD |
| --- | --- | --- | --- |
| High-harmonic target | 1 | 2 | 0.0513 +/- 0.0000 |
| High-harmonic target | 2 | 4 | 0.1185 +/- 0.0024 |
| High-harmonic target | 3 | 6 | 0.0813 +/- 0.0554 |
| High-harmonic target | 4 | 8 | 0.0431 +/- 0.0084 |
| High-harmonic target | 5 | 10 | 0.0322 +/- 0.0090 |
| High-harmonic target | 6 | 12 | 0.0100 +/- 0.0078 |
| Original target | 1 | 2 | 0.0659 +/- 0.0000 |
| Original target | 2 | 4 | 0.1466 +/- 0.0004 |
| Original target | 3 | 6 | 0.0150 +/- 0.0000 |
| Original target | 4 | 8 | 0.0080 +/- 0.0076 |
| Original target | 5 | 10 | 0.0017 +/- 0.0014 |
| Original target | 6 | 12 | 0.0014 +/- 0.0012 |

The 1D results are inherited from the executed Week 1 Advancement notebook and are not refit here. The original target improves from approximately 0.0659 at L=1 to 0.00138 at L=6. The high-harmonic target improves to approximately 0.0100 at L=6, with greater seed variability.

### 4.2 Classical 2D baselines and QNN layer sweep
| Model | Parameters | 64x64 grid MSE |
| --- | --- | --- |
| Fourier linear |k_j|<=3 | 49 | 3.3e-31 |
| MLP 2-12-1 | 49 | 9.58e-05 |

| L | Params | Serial MSE mean +/- SD | Parallel MSE mean +/- SD | Parallel |2c(1,-1)| |
| --- | --- | --- | --- | --- |
| 1 | 2 | 0.4203 +/- 0.0001 | 0.1702 +/- 0.0000 | 0.000 |
| 2 | 4 | 0.2583 +/- 0.0410 | 0.1700 +/- 0.0000 | 0.000 |
| 3 | 6 | 0.1716 +/- 0.0248 | 0.1586 +/- 0.0126 | 0.236 |
| 4 | 8 | 0.1770 +/- 0.0621 | 0.1166 +/- 0.0034 | 0.209 |
| 5 | 10 | 0.1274 +/- 0.0183 | 0.0788 +/- 0.0104 | 0.164 |
| 6 | 12 | 0.1562 +/- 0.0259 | 0.0673 +/- 0.0061 | 0.177 |

The Fourier baseline recovers the target to numerical precision. The matched-size MLP reaches a small but nonzero error. In the QNN sweep, parallel performance improves with L and reaches 0.0673 mean grid MSE at L=6; serial reaches 0.1562. The learned mixed-mode magnitude is nonzero for the parallel L=3-6 models, while L=1-2 suppress it. These outcomes distinguish candidate support from successful coefficient learning.

### 4.3 Fourier spectrum and support
Across 60 trained 2D models, the summed count of coefficients beyond the threshold is 0 on the 64x64 grid and 0 on the 128x128 grid. All measured active modes remained within the declared coordinate-wise support for the tested layers. The refined grid gives the same grid MSE values to the displayed precision, supporting that the reported errors are not a coarse-grid aliasing artifact.

### 4.4 Depth and CNOT ablations
| Condition | Grid MSE mean +/- SD | |2c(1,-1)| mean | Outside modes: 64 / 128 |
| --- | --- | --- | --- |
| Parallel L=3 deeper, fixed 3 encodings | 0.0822 +/- 0.0053 | 0.065 | 0 / 0 |
| Parallel L=3 without CNOT | 0.1704 +/- 0.0001 | 0.000 | 0 / 0 |
| Parallel L=3 reference | 0.1586 +/- 0.0126 | 0.236 | 0 / 0 |

With three encodings and six unique trainable scalars held fixed, the deeper architecture lowers MSE relative to the reference. It uses 12 trainable rotation occurrences (six shared scalars), six CNOTs, and logical depth 15; the reference uses six trainable rotation occurrences, three CNOTs, and logical depth 9. Removing CNOTs reduces the mixed-mode amplitude to numerical zero in this circuit and worsens the fit. The result is specific to these layouts and training settings.

### 4.5 Two-spiral classification
| Model | Parameters | Accuracy mean +/- SD | Macro-F1 mean +/- SD |
| --- | --- | --- | --- |
| Fourier logistic |k_j|<=4 | 81 | 0.611 +/- 0.031 | 0.611 +/- 0.031 |
| MLP 2-1-1 (parameter matched) | 5 | 0.533 +/- 0.042 | 0.481 +/- 0.055 |
| 2-qubit re-uploading QNN L=3 | 6 | 0.519 +/- 0.057 | 0.519 +/- 0.057 |

The 81-feature Fourier logistic baseline gives the best mean accuracy and macro-F1 across the shared folds. The compact QNN is close to the parameter-matched MLP in accuracy, but neither matches the Fourier model on this dataset. The QNN result is therefore a small-model benchmark, not evidence for a general quantum-classification advantage.

### 4.6 Aer depolarizing noise and finite shots
| Layout | p per gate | Target MSE mean +/- SD | MSE to noiseless | Mean abs. bias |
| --- | --- | --- | --- | --- |
| Serial | 0 | 0.3053 +/- 0.0017 | 0.00075 | 0.0216 |
| Serial | 0.001 | 0.3004 +/- 0.0000 | 0.00079 | 0.0222 |
| Serial | 0.005 | 0.2837 +/- 0.0000 | 0.00157 | 0.0333 |
| Serial | 0.01 | 0.2668 +/- 0.0000 | 0.00372 | 0.0513 |
| Parallel | 0 | 0.1682 +/- 0.0020 | 0.00095 | 0.0249 |
| Parallel | 0.001 | 0.1700 +/- 0.0000 | 0.00099 | 0.0258 |
| Parallel | 0.005 | 0.1683 +/- 0.0000 | 0.00110 | 0.0267 |
| Parallel | 0.01 | 0.1664 +/- 0.0000 | 0.00152 | 0.0312 |

Each repeat contains 262,144 shots over 256 points; the experiment includes 40 layout/rate repeats. Target MSE is not monotonic in p because stochastic errors can partially offset a model's deterministic target-fit error. The direct deviation from the noiseless prediction and absolute bias rise with noise, more strongly in the serial case. This p=0 reference still includes shot sampling.

## 5. Observations and limitations
- More re-upload layers increase candidate support, but fitting the target coefficients remains an optimization problem. Layer count alone does not guarantee lower error.
- The parallel layout represents the mixed target mode more effectively in this ansatz and has lower L=6 error than the serial layout, at the cost of one CNOT per layer.
- No support falsifier was triggered under the stated threshold and both grid resolutions. This is evidence for these circuits, target, and sampling resolutions rather than a universal theorem.
- Two-qubit circuits are classically simulable at this scale. No quantum-advantage claim is made.
- The depth ablation changes gate occurrences, entanglers, and repeated parameter use while holding the number of unique trainables and feature encodings fixed. It is an architectural control, not an isolated universal depth law.
- The Aer channel is depolarizing and does not include device calibration drift, crosstalk, readout asymmetry, hardware compilation, or backend-specific noise. No hardware circuit was run in Week 2.
- Spiral classification uses one compact QNN design, 300 QNN updates per fold, and five saved folds. The result should not be generalized to all quantum classifiers.

## 6. Week 3 plan
Check backend access and calibration; freeze a trained one-qubit L=3 regressor; evaluate 64 periodic points with 1,024 hardware shots; compare the hardware curve against finite-shot Aer and the noiseless statevector; record backend name, calibration date, transpiled depth, gate counts, and shot totals.

## References
1. A. Pérez-Salinas et al., Data re-uploading for a universal quantum classifier, Quantum 4, 226 (2020). DOI: 10.22331/q-2020-02-06-226.
2. M. Schuld, R. Sweke, and J. J. Meyer, Effect of data encoding on the expressive power of variational quantum machine learning models, Physical Review A 103, 032430 (2021). DOI: 10.1103/PhysRevA.103.032430.

## Appendix A. Figure index
The notebook saves the 1D reused sweep, 2D layer sweep, fitted surfaces, Fourier spectra, noise curve, ablation comparison, spiral model scores, and spiral decision boundaries under outputs/week2/figures/.
