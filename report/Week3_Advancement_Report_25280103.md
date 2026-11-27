# Week 3 Advancement Report — Data Re-uploading and the Fourier Spectrum of QNNs

**Student:** Rana Muhammad Hamza
**Roll number:** 25280103
**Project:** Project 9 — Data re-uploading and the Fourier spectrum of QNNs
**Date:** 28 November 2026

## Executive summary

This separate Week 3 advancement notebook extends the completed Week 1 and Week 2 experiments without changing their notebooks. It makes one reproducible cross-week hardware plan: the saved one-qubit 1D models at depths L = 1, 2, 3, and 6, the saved 2D serial and parallel encoders at L = 3, and a small balanced spiral audit sample. The notebook builds the exact circuits, records an input-to-circuit plan, computes noiseless statevector reference values, and submits a batched IBM Quantum workload.

The regression/depth/layout workload completed on IBM Quantum backend `ibm_marrakesh` as job `dc4v1o5s2omc738g26e0`. It contained 256 circuits at 512 shots per circuit; the IBM platform showed 0.61 RUs. The platform status is verified. IBM rejected the runtime credential when the completed job was reopened for raw-count recovery, so this package deliberately reports no invented hardware MSE, MAE, accuracy, or Fourier coefficients for the advancement run. The spiral follow-up was not submitted after that credential failure.

## 1. Introduction and research question

Data re-uploading lets a compact variational circuit encode the input repeatedly. The central Week 3 question is: **how do encoding repetitions, circuit depth, and encoding layout affect the frequencies that a QNN can represent?** The advancement focuses on an auditable hardware bridge: use the same trained parameters already saved by Weeks 1–2, evaluate those circuits on IBM hardware, and preserve the exact circuit/input mapping so that the hardware curve can be reconstructed when raw counts are available.

## 2. Paper basis and hypothesis

The design follows Pérez-Salinas et al. (Quantum 4, 226, 2020), which motivates data re-uploading as a way for a small circuit to build expressive models, and Schuld, Sweke, and Meyer (Physical Review A 103, 032430, 2021), which connects data-encoding structure with the Fourier spectrum of a quantum model.

**Hypothesis.** Increasing re-uploading depth should make more Fourier components available, while the serial and parallel layouts should produce different spectral support and hardware sensitivity. Finite-shot sampling and device noise should perturb the fitted curve but should not change the planned frequency support of the noiseless circuit.

## 3. Advancement scope

| Component | Frozen model/evaluation | Purpose |
| --- | --- | --- |
| Week 1 1D | One-qubit original target at L = 1, 2, 3, 6, seed 3, 32 inputs/model | Depth and frequency audit |
| Week 2 2D | Serial and parallel L = 3, seed 0, 8×8 grid | Encoding-layout comparison |
| Week 2 spiral | Parallel L = 3, fold 0, balanced 64-example sample | Small classification hardware audit |
| Hardware | IBM `ibm_marrakesh`, 512 shots/circuit | Hardware validation |

The complete planned design has 320 circuits: 128 1D circuits, 128 2D layout circuits, and 64 spiral circuits. The first IBM submission contains the 256 regression/layout circuits. The notebook records the remaining 64-circuit spiral follow-up as pending rather than silently dropping it.

## 4. Methodology and experimental setup

1. Load the previously saved parameters, scaling, targets, and dataset splits from the existing Week 1/2 outputs.
2. Rebuild the same one-qubit and two-qubit angle-embedding/re-uploading circuits. No trained weights are changed.
3. Evaluate exact statevector expectations locally and save them in `week3_advancement_reference_predictions.csv`.
4. Create `week3_advancement_experiment_plan.csv`, which maps every circuit to experiment, model, depth, layout, input, target, and label.
5. Submit circuits to IBM Runtime in one bounded batch with the recorded shot count.
6. Recover counts, compare hardware predictions to the noiseless reference, and compute curve/accuracy metrics when a valid IBM runtime credential is available.

The notebook is intentionally defensive: an already completed job is recovered by job ID rather than resubmitted, and a failed raw-result recovery creates a clear note instead of fabricating metrics.

## 5. IBM Quantum execution evidence

| Field | Recorded value |
| --- | --- |
| Backend | `ibm_marrakesh` |
| IBM job | `dc4v1o5s2omc738g26e0` |
| Circuits in completed workload | 256 |
| Shots per circuit | 512 |
| Platform status | Completed |
| Platform usage | 0.61 RUs |
| Raw counts recovered by this run | No |
| Spiral follow-up | Not submitted |

The authenticated IBM Quantum workload overview is included in the PDF. It is platform-status evidence, not a substitute for raw count tables.

## 6. Results available in this package

The notebook ran successfully with zero cell errors and produced the following auditable artifacts:

| Artifact | What it contains |
| --- | --- |
| `week3_advancement_reference_predictions.csv` | Noiseless reference expectations and targets for the planned points |
| `week3_advancement_experiment_plan.csv` | Circuit/input/target mapping for reproducibility |
| `week3_advancement_regression_submission.json` | IBM job ID, backend, circuit count, shots, and submission time |
| `week3_advancement_execution_status.json` | Completion state and raw-result availability |
| `week3_advancement_hardware_note.json` | Explicit IBM credential recovery note |
| `week3_advancement_spiral_note.json` | Explicit pending spiral submission note |
| `figures/ibm_quantum_platform_workload_overview.png` | IBM platform evidence capture |

No raw-result metrics are claimed for this advancement run because the supplied API key was rejected during result recovery. This is a reproducibility limitation, not a numerical result.

## 7. Limitations and observations

- The completed IBM regression workload is verifiable by job ID and platform status, but its counts could not be downloaded with the credential available in this run.
- The spiral follow-up remains pending and must be submitted only after a valid IBM Quantum API key is supplied.
- The 320-circuit design is intentionally bounded for a student-scale hardware experiment; it is not a full device-wide benchmark.
- Hardware comparisons should be reported only after count recovery, with confidence intervals or repeated shots where possible.
- Credentials are not stored in the repository. Because an API key was pasted in chat earlier, it should be rotated/revoked and replaced with a fresh key before rerunning.

## 8. Week 3 completion and next action

The separate advancement notebook, local reference outputs, experiment plan, IBM submission record, platform evidence image, and this report are complete and packaged. The notebook itself executes cleanly. The only outstanding scientific action is credential-dependent: recover the completed regression counts and submit the 64-circuit spiral follow-up, then let the existing analysis cells generate hardware metrics without changing the experimental design.

## References

1. M. Pérez-Salinas et al., “Data re-uploading for a universal quantum classifier,” *Quantum* 4, 226 (2020). DOI: 10.22331/q-2020-02-06-226.
2. M. Schuld, R. Sweke, and J. J. Meyer, “Effect of data encoding on the expressive power of variational quantum-machine-learning models,” *Physical Review A* 103, 032430 (2021). DOI: 10.1103/PhysRevA.103.032430.
