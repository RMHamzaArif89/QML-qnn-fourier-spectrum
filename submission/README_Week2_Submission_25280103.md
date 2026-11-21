# Project 9 — Week 2 Submission

**Student:** Rana Muhammad Hamza  
**Roll number:** 25280103  
**Course:** QML  
**Milestone:** Week 2 simulator results, noise model, ablations, and report draft

## Research focus

This submission studies how data re-uploading and encoding layout affect the Fourier frequencies and regression performance of small quantum neural networks. It includes the 1D Week 1 layer results reused for continuity, 2D serial and parallel models, Fourier support checks, depth and entanglement ablations, two-spiral classification, and finite-shot Aer depolarizing-noise results.

## Contents

- notebooks/25280103_Week2_Simulator_Results.ipynb — complete Week 2 notebook.
- outputs/week2/ — saved tables, figures, trained parameters, predictions, and run configuration.
- report/Week2_Results_Draft_25280103.pdf and .md — formatted results draft and its editable source.
- outputs/week1/week1_inputs_and_fixed_folds.npz — fixed synthetic data and classification folds used by Week 2.
- outputs/week1Advancement/ — the completed 1D L=1–6 sweep and configuration reused by Week 2.
- synopsis.tex and Project_9_Synopsis_25280103_RMHamza.pdf — project synopsis reference.
- requirements.txt — Python package requirements.

## Reproducing the notebook

From the extracted archive root, install the packages in requirements.txt, open the notebook with the project Python/Jupyter kernel, and run all cells. The notebook reads the included Week 1 data and 1D advancement tables, then writes generated Week 2 results beneath outputs/week2/.

All Week 2 model and noise experiments in this submission use local statevector or Qiskit Aer simulation. Hardware evaluation is planned for Week 3 and is not claimed as completed here.
