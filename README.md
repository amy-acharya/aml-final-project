# Fold or Fail: Predicting Protein Stability Changes from Mutations
Can graph neural networks learn what sequence alone cannot?

This repository contains our Applied Machine Learning final project. We study whether graph neural networks (GNNs) on protein residue contact graphs improve prediction of mutation-induced protein stability changes, measured as ΔΔG, beyond tabular baselines.

Our central motivating question was if residue contact graphs add useful structural information for ΔΔG prediction beyond mutation-level and condition-aware flat features. 

```text
index.html

To render our project site locally: clone or download this repository, open the repository folder, and open index.html in Google Chrome. 


## Project Overview
A single amino acid mutation can stabilize or destabilize a protein. We model this as a supervised regression problem:

- **Input:** single-point protein mutation features, experimental conditions, and/or residue contact graphs
- **Output:** ΔΔG in kcal/mol (a continuous numeric value)
- **Objective:** predict continuous stability change
- **Metrics:** RMSE and Pearson correlation

We compare two modeling approaches:

1. **XGBoost / tabular baselines**  
   Models using mutation-level physicochemical and experimental features.

2. **Graph neural networks**  
   Models trained on protein residue graphs where nodes are amino acids and edges represent sequence or structural contacts.

Our driving question was if GNNs improve accuracy, and when graph structure becomes more useful for exploring structural relationships in protein data. 

## Repository Structure
## Repository Structure

```text
aml-final-project/
├── index.html
├── README.md
├── single_point_mutations.tsv
│
├── 01_data_exploration_xgboost_baseline.ipynb
├── 02_gnn.ipynb
├── 03_reproduce_blog_figures.ipynb
│
├── assets/
│   ├── figures/
│   │   └── final blog-ready figure images
│   ├── contact_graph_example_final_main.json
│   └── xgb_training_and_test_performance_xgb_prototype.png
│
└── results/
    ├── xgboost/
    │   └── saved XGBoost metrics, predictions, training curves, and feature importances
    │
    ├── all_predictions_final_main.csv
    ├── all_predictions_with_context_final_main.csv
    ├── asa_stratified_results_final_main.csv
    ├── baseline_results_final_main.csv
    ├── cleaned_data_with_splits_final_main.csv
    ├── gnn_seed_results_final_main.csv
    ├── gnn_summary_results_final_main.csv
    ├── graph_coverage_final_main.csv
    ├── label_distribution_final_main.csv
    ├── model_comparison_final_main.csv
    ├── model_ranking_final_main.csv
    ├── tabular_results_final_main.csv
    ├── training_history_final_main.csv
    ├── v4_seed_results_final_main.csv
    └── v4_summary_results_final_main.csv