# LLM Logical Reasoning Evaluation: Do LLMs Reason or Imitate?

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Platform: Kaggle](https://img.shields.io/badge/Platform-Kaggle-blue.svg)](https://www.kaggle.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

## 📌 Project Overview
This repository contains the implementation of a falsifiable experimental framework designed for the **Expert Systems** final project. The core objective is to investigate whether Large Language Models (LLMs) genuinely perform First-Order Logic (FOL) reasoning (e.g., Unification, Generalized Modus Ponens) or if they merely imitate statistical linguistic patterns derived from their pre-training data.

This project moves beyond standard accuracy benchmarks by designing a rigid pipeline that separates **random statistical/linguistic noise** from **systematic structural logic errors**.

## 🔬 Core Hypotheses
The framework specifically tests the following two hypotheses:

*   **H1 (Effect of Prior Knowledge & Surface Alterations):** The logical reasoning performance of the LLM significantly drops when surface-level features are altered. This is tested by replacing real-world entities with meaningless/fictional symbols (neutralizing prior knowledge) and by reordering logical premises without changing the underlying logical structure.
*   **H2 (Quantifier Scoping Comprehension):** The model systematically fails to distinguish between logical formulations with swapped quantifiers (e.g., $\forall x \exists y$ vs. $\exists y \forall x$) when the surface syntax remains nearly identical.

## 🗂️ Repository Structure
In accordance with the project requirements, the repository is organized as follows to ensure full reproducibility:

```text
├── data/                   # Raw and processed datasets (Neutral/Caroline datasets, etc.)
├── notebooks/              # Executable Kaggle Notebooks for experiments
│   ├── 01_H1_Neutral_Data_Generator.ipynb
│   ├── 02_H2_Quantifier_Surprisal.ipynb
│   └── 03_Z3_Formal_Verification.ipynb
├── results/                # Raw experimental data, logs, and statistical analysis scripts
├── plots/                  # Generated plots distinguishing random vs. systematic errors
├── docs/                   # Documentation and reports
│   ├── Final_Paper.pdf     # The main research report (IEEE/Standard format)
│   ├── AI_Usage_Report.pdf # Detailed appendix of AI tools used (per course policy)
│   └── Presentation.pdf    # Slides for the final defense
└── README.md               # Project documentation and reproduction guide
