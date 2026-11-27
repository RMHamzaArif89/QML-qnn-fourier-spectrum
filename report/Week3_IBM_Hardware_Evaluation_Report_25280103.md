# Week 3 IBM Quantum Hardware Evaluation

**Student:** Rana Muhammad Hamza  
**Roll number:** 25280103

## Result at a glance

The frozen Week 1 one-qubit L=3 re-uploading QNN (seed 3) was executed on IBM backend `ibm_marrakesh` across 64 inputs with 1,024 shots per circuit, for 65,536 total hardware shots. IBM Runtime job: `dc2uakinj2vs73dhbtjg`.

| Execution | MSE to target | MAE to target | MAE to noiseless |
| --- | ---: | ---: | ---: |
| Noiseless statevector | 3.68e-06 | 0.0017 | 0.0000 |
| Aer finite-shot | 0.000923 | 0.0241 | 0.0235 |
| IBM hardware | 0.000839 | 0.0222 | 0.0226 |

The complete professional report is available as the accompanying PDF. Raw counts, predictions, figures, and metadata are in `outputs/week3/`. Credentials are not included anywhere in project artifacts.
