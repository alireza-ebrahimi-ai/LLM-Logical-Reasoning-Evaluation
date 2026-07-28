# The Illusion of Inference: A Neuro-Symbolic Falsification of LLM Reasoning

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-orange)
![Z3 Solver](https://img.shields.io/badge/Formal_Verification-Z3_SMT_Solver-red)
![Kaggle](https://img.shields.io/badge/Environment-Kaggle_T4x2_GPU-20BEFF)
![License](https://img.shields.io/badge/License-MIT-green)

## Overview
This repository contains the full source code, datasets, formal verification scripts, and experimental results for the final project in the **Advanced Expert Systems** course at **Yazd University**. 

The study investigates a fundamental question in modern Artificial Intelligence: **Do Large Language Models (LLMs) execute genuine deductive reasoning, or do they merely mimic statistical token patterns?**

To answer this, we establish a falsifiable neuro-symbolic framework combining natural language semantic neutralization, SMT theorem proving with the **Z3 Solver**, and raw PyTorch token surprisal extraction across three distinct model families.

---

## Key Empirical Findings

### 1. Hypothesis 1: Invariance to Surface Perturbations (H1)
When real-world entities in the FOLIO dataset were replaced with synthetic nonsense tokens (the "Caroline Filter"), the logical structure remained **100% mathematically invariant** (certified by Z3). However, LLM reasoning accuracy collapsed across all evaluated architectures:
*   **Qwen2.5-7B-Instruct:** Accuracy dropped from **56.86%** to **44.61%** ($\Delta = -12.25\%$)
*   **Gemma-2-2B-It:** Accuracy dropped from **52.45%** to **41.18%** ($\Delta = -11.27\%$)
*   **Mistral-7B-Instruct-v0.2:** Accuracy dropped from **45.59%** to **37.75%** ($\Delta = -7.84\%$)

### 2. Hypothesis 2: Systematic Quantifier Scoping (H2)
Evaluating 50 procedurally generated minimal pairs testing quantifier scope ambiguity ($\forall x \exists y$ vs. $\exists y \forall x$) via raw conditional token surprisal ($-\log P$) revealed chaotic, non-systematic probability distributions. Models react to local token co-occurrence (lexical heuristics) rather than formal quantifier syntax.

---

## Evaluated LLM Families
We benchmarked three diverse, open-weights model families on dual NVIDIA T4 GPUs:
1.  **Qwen2.5-7B-Instruct** (Alibaba Cloud)
2.  **Gemma-2-2B-It** (Google)
3.  **Mistral-7B-Instruct-v0.2** (Mistral AI)

---

## Repository Structure

```
├── data/
│   ├── folio_raw_original.jsonl           # Baseline raw FOLIO dataset
│   ├── folio_h1_caroline.csv              # Neutralized H1 dataset (Caroline filter)
│   ├── llm_answers_h1_qwen.csv            # H1 inference outputs (Qwen2.5)
│   ├── llm_answers_h1_gemma.csv           # H1 inference outputs (Gemma-2)
│   ├── llm_answers_h1_mistral.csv         # H1 inference outputs (Mistral-v0.2)
│   ├── h2_synthetic_minimal_pairs.csv     # 50 unique minimal pairs dataset
│   ├── surprisal_results_h2_all_models.csv# Raw PyTorch token surprisal scores
│   └── z3_h1_proof_log.txt                # Z3 formal logic verification proof log
├── notebooks/
│   ├── 01_dataset_preparation_H1.ipynb    # Data downloading & Caroline NER filtering
│   ├── 02_llm_inference_H1.ipynb          # Multi-model zero-shot H1 inference
│   ├── 03_z3_verifier_H1.ipynb            # Z3 SMT formal proof by contradiction
│   ├── 04_llm_surprisal_H2.ipynb          # Minimal pairs & PyTorch logit surprisal extraction
│   └── 05_statistical_analysis.ipynb      # Statistical aggregation & Vector PDF generation
├── results/
│   ├── h1_accuracy_drop_all_models.pdf    # Vector PDF plot for H1 results
│   └── h2_surprisal_inconsistency_all_models.pdf # Vector PDF plot for H2 results
├── docs/
│   ├── NeuroSymbolic_LLM_Reasoning_Evaluation.pdf # Main paper
│   ├── AI_Usage_Report.pdf                # Standalone AI Usage Audit Appendix
│   └── presentation_slides.pdf            # 13-slide Beamer deck for oral defense
└── README.md                              # This documentation file
```

---

## Reproducibility & Execution

All experiments are fully reproducible in a standard Python / Kaggle environment.

### Prerequisites
```bash
pip install torch transformers z3-solver spacy pandas matplotlib seaborn
python -m spacy download en_core_web_sm
```

### Execution Steps
1.  **Data Generation:** Run `notebooks/01_dataset_preparation_H1.ipynb` to download FOLIO and apply entity replacement.
2.  **H1 Evaluation:** Run `notebooks/02_llm_inference_H1.ipynb` to collect model decisions across Qwen, Gemma, and Mistral.
3.  **Formal Proof:** Run `notebooks/03_z3_verifier_H1.ipynb` to execute the Z3 SMT solver and verify logical invariance.
4.  **H2 Surprisal:** Run `notebooks/04_llm_surprisal_H2.ipynb` to generate minimal pairs and extract PyTorch logits.
5.  **Plot Generation:** Run `notebooks/05_statistical_analysis.ipynb` to generate the publication-ready vector PDF figures.

---

## Authors & Citation

*   **Alireza Ebrahimi** - Department of Computer Science, Yazd University (`alireza.ebrahimi@stu.yazd.ac.ir`)
*   **Jamal Zarepour-Ahmadabadi** (Instructor) - Department of Computer Science, Yazd University (`zarepourjamal@yazd.ac.ir`)

```bibtex
@article{ebrahimi2026illusion,
  title={The Illusion of Inference: A Neuro-Symbolic Falsification of LLM Reasoning via Formal Verification and Token Surprisal},
  author={Ebrahimi, Alireza and Zarepour-Ahmadabadi, Jamal},
  journal={Expert Systems with Applications (Under Review)},
  year={2026}
}
```
