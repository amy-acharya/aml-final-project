# Fold or Fail: Predicting Protein Stability Changes from Mutations

This repository contains our Applied Machine Learning final project. We study whether graph neural networks (GNNs) on protein residue contact graphs improve prediction of mutation-induced protein stability changes, measured as ΔΔG, beyond strong tabular baselines such as XGBoost and HistGradientBoosting.

## Project Overview

A single amino acid mutation can change how stable a protein is. Our task is to predict ΔΔG from single-point mutation data.

We compare two modeling approaches:

1. **Tabular baselines**  
   Models trained on mutation-level physicochemical and experimental features.

2. **Graph neural networks**  
   Models trained on protein residue graphs where nodes are amino acids and edges represent sequence or structural contacts.

The central question is not only whether GNNs improve accuracy, but **when graph structure helps and when strong engineered tabular features remain competitive**.

## Repository Structure

```text
aml-final-project/
├── index.html                         # final HTML blog post
├── README.md
├── single_point_mutations.tsv          # raw mutation dataset
├── final_reproducible_figures.ipynb    # notebook that regenerates blog figures
├── project.ipynb                       # XGBoost baseline/prototype notebook
├── GNN_v2_zkedited.ipynb               # GNN training/evaluation notebook
│
├── results/
│   ├── xgboost/                        # saved XGBoost outputs
│   ├── model_comparison_final_main.csv
│   ├── all_predictions_final_main.csv
│   ├── asa_stratified_results_final_main.csv
│   ├── training_history_final_main.csv
│   └── ...
│
└── assets/
    ├── figures/                        # final blog-ready figures
    └── contact_graph_example_final_main.json