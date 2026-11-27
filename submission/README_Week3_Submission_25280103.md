# Week 3 Submission - IBM Quantum Hardware Evaluation

**Student:** Rana Muhammad Hamza  
**Roll number:** 25280103  
**Project:** Data re-uploading and the Fourier spectrum of QNNs

## Submission scope

This archive contains the complete Week 3 deliverable:

- the executed Week 3 notebook;
- the professional PDF report and editable Markdown report;
- the IBM Quantum hardware result bundle, including raw counts, predictions, metrics, figures, backend/job metadata, and transpiled resource counts;
- the project requirements file and setup notes.

The Week 3 experiment evaluates the frozen one-qubit, three-layer QNN selected from Week 1 on IBM backend `ibm_marrakesh`. It uses 64 periodic inputs and 1,024 shots per input, for 65,536 total hardware shots. The completed Runtime job is recorded as `dc2uakinj2vs73dhbtjg`.

## Requirement coverage

Week 1 establishes the data pipeline, classical baselines, first QNN, and Fourier-spectrum analysis. Week 2 supplies the simulator layer sweep, serial/parallel encoding comparison, noise study, ablations, and spiral classification. The schedule specifically assigns the IBM hardware result to Week 3; therefore, separate hardware reruns of every Week 1 and Week 2 simulator experiment are not required for this milestone.

## How to review

1. Open `notebooks/25280103_Week3_IBM_Hardware_Evaluation.ipynb` with the QNN Fourier Spectrum kernel.
2. Review the executed outputs and the files under `outputs/week3/`.
3. Read `report/Week3_IBM_Hardware_Evaluation_Report_25280103.pdf` for the presentation-ready summary.

No IBM API key, CRN, password, or other credential is included in this archive.
