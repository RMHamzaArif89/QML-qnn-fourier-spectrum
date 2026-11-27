# Week 3 advancement - cross-week IBM Quantum validation

This folder belongs to the separate notebook `notebooks/25280103_Week3_Advancement.ipynb`. It does not replace or modify the Week 1, Week 2, or original Week 3 notebooks.

## Scope

- Week 1 1D saved models: original target at L = 1, 2, 3, and 6, seed 3.
- Week 2 2D saved models: serial and parallel layouts at L = 3, seed 0.
- Week 2 spiral model: parallel L = 3, fold 0, balanced 64-example audit sample.
- IBM backend: `ibm_marrakesh`, 512 shots per circuit.

## IBM execution status

The regression/depth/layout workload was submitted and completed on IBM Quantum as job `dc4v1o5s2omc738g26e0` with 256 circuits and 512 shots per circuit. The platform reported completion and 0.61 RUs. Its submission record is retained in `week3_advancement_regression_submission.json` and the completion state is recorded in `week3_advancement_execution_status.json`.

The runtime API key supplied for this recovery attempt was rejected by IBM when retrieving the completed job result. Therefore the notebook deliberately does not invent raw hardware predictions or metrics. The 64-circuit spiral follow-up was not submitted. Re-running the notebook with a valid IBM Quantum API key will recover the completed regression result and submit the spiral follow-up without resubmitting the completed regression job.

## Files

- `week3_advancement_experiment_plan.csv`: exact circuit-to-model/input mapping.
- `week3_advancement_reference_predictions.csv`: local noiseless expectations and targets.
- `week3_advancement_regression_submission.json`: credential-free IBM submission record.
- `week3_advancement_execution_status.json`: completion and recovery status.
- `week3_advancement_hardware_note.json`, `week3_advancement_spiral_note.json`: explicit recovery notes.
- `figures/ibm_quantum_platform_workload_overview.png`: authenticated IBM platform evidence capture.

No IBM API key or CRN is stored in this folder.
