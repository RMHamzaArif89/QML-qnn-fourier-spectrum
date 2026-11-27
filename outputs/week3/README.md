# Week 3 IBM Hardware Evaluation

**Student:** Rana Muhammad Hamza<br>
**Roll number:** 25280103<br>
**Milestone:** Week 3 hardware validation

This folder contains a real IBM Quantum hardware evaluation of the frozen Week 1, one-qubit L=3 re-uploading regressor. The selected parameters are the saved L=3, seed 3 model because it had the lowest Week 1 dense-grid MSE. It is evaluated at 64 periodic inputs with 1,024 shots per input and compared against exact statevector and finite-shot Aer results.

**Backend:** `ibm_marrakesh`<br>
**Runtime job ID:** `dc2uakinj2vs73dhbtjg`

## Files

- `week3_hardware_predictions.csv`: target, noiseless, Aer, and hardware expectations at every input.
- `week3_hardware_summary.csv`: error metrics.
- `week3_hardware_counts.json`: raw one-qubit measurement counts.
- `week3_job_metadata.json`, `week3_backend_metadata.json`, and `week3_circuit_resources.csv`: execution and resource record.
- `week3_run_config.json`: frozen-model and reproducibility configuration.
- `figures/`: comparison and deviation figures.

No IBM API key, CRN, or other credential is stored in this folder.
