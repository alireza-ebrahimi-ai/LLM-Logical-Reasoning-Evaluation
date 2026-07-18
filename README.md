# Do LLMs Really "Reason" or Just Mimic? A Falsifiable Neuro-Symbolic Framework

![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![Kaggle](https://img.shields.io/badge/Environment-Kaggle-20BEFF)
![Z3 Solver](https://img.shields.io/badge/Formal_Verification-Z3_SMT_Solver-red)

## Overview
This repository contains the codebase, datasets, and experimental results for the final project in the Expert Systems course. The project investigates a fundamental question in modern Artificial Intelligence: **Do Large Language Models (LLMs) perform actual logical deduction, or do they merely reproduce statistical linguistic patterns?**

To answer this, we introduce a falsifiable, neuro-symbolic evaluation framework that tests LLMs against First-Order Logic (FOL) principles, strictly separating statistical language errors from true systematic logic errors.

## Core Hypotheses
This project designs and executes a rigorous experimental pipeline to test two specific hypotheses:

*   **H1 (Effect of Surface-level Perturbations):** The logical reasoning performance of LLMs drops significantly when evaluating logically equivalent inferences that have altered surface structures (e.g., replacing real-world entities with nonsense/neutral words to eliminate the effect of prior knowledge, or permuting the order of premises).
*   **H2 (Quantifier Scoping Failures):** LLMs systematically fail to distinguish between formulations with swapped quantifiers (e.g., $\forall x \exists y$ versus $\exists y \forall x$) that possess nearly identical surface linguistic structures.

## System Architecture
The evaluation pipeline is divided into three main phases:

1.  **Neutral Dataset Generation (The "Caroline" Filter):** Automatically replacing entities, verbs, and nouns in standard logical datasets (e.g., FOLIO) with synthetic tokens to neutralize inherent cognitive biases.
2.  **LLM Inference & Surprisal Analysis:** Querying models and using tools like `minicons` to calculate token surprisal rates, isolating random statistical noise from systematic behavior.
3.  **Formal Verification (Z3 Prover):** Translating the intermediate reasoning steps of the LLM into Python-executable First-Order Logic formulas and verifying them using the **Z3 SMT Solver** ($M \models \alpha$).

## Repository Structure
  /data                   --> Contains raw datasets and generated neutral datasets
  /notebooks              --> Kaggle executable notebooks (Data generation, LLM API calls, Z3 Verification)
  /results                --> Raw experimental logs, statistical analysis, and generated plots
  /docs                   --> Final academic paper, presentation slides, and the AI Usage Appendix
  README.md               --> This file

## Reproducibility and Execution
This project is designed to be fully reproducible and is optimized for the **Kaggle** environment. 

### Dependencies
To run the notebooks, ensure the following packages are installed in your Kaggle environment:
*   z3-solver
*   minicons
*   transformers
*   pandas, matplotlib, seaborn (for statistical analysis)

### Execution Steps
1.  Run the `01_dataset_generation.ipynb` notebook to generate the neutral and quantifier-swapped datasets.
2.  Run the `02_llm_inference.ipynb` notebook to collect responses and calculate token probabilities.
3.  Run the `03_z3_formal_verification.ipynb` notebook to evaluate the logical soundness of the outputs.
4.  Run the `04_statistical_analysis.ipynb` to generate the final comparative plots and error classifications.

## Academic Integrity & AI Usage
In compliance with the course policies, all commits in this repository reflect the incremental progress of the project. A detailed appendix regarding the transparent use of AI-assisted tools for code generation and text editing is included in the `/docs` directory.

## References
This framework builds upon state-of-the-art neuro-symbolic research, including:
*   *FoVer: First-Order Logic Verification for Natural Language Reasoning*
*   *Evaluating the Robustness of Analogical Reasoning in Large Language Models*
