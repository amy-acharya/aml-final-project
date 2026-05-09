# Fold or Fail: Predicting Protein Stability Changes from Mutations
Can graph neural networks learn what sequence alone cannot?

This repository contains our Applied Machine Learning final project. We study whether graph neural networks (GNNs) on protein residue contact graphs improve prediction of mutation-induced protein stability changes, measured as ΔΔG, beyond tabular baselines.

Our central motivating question was if residue contact graphs add useful structural information for ΔΔG prediction beyond mutation-level and condition-aware flat features. 

## How to View the Final HTML Blog

The final website is contained in:

```text
index.html
```

To render the project locally:

1. Clone or download this repository.
2. Open the repository folder.
3. Open `index.html` in Google Chrome.

On macOS, this can also be done from Terminal:

```bash
cd path/to/aml-final-project
open -a "Google Chrome" index.html
```

The HTML site uses local files only. Figures are stored in `assets/figures/`, saved model outputs are stored in `results/`, and the interactive protein structure viewer uses a local copy of `3Dmol.js` stored in `assets/js/`. 

## How to Reproduce the Blog Figures

To regenerate the figures used in the blog, run:

```text
03_reproduce_blog_figures.ipynb
```

This notebook loads saved model outputs from the `results/` folder and regenerates the figures used in `index.html`. It does **not** require rerunning the full XGBoost or GNN training pipelines.

The notebook reads from:

```text
single_point_mutations.tsv
results/
results/xgboost/
assets/
```

and saves figure outputs to:

```text
assets/figures/
```

## Project Overview

A single amino acid mutation can stabilize or destabilize a protein. We model this as a supervised regression problem:

- **Input:** single-point protein mutation features, experimental conditions, and/or residue contact graphs
- **Output:** ΔΔG in kcal/mol
- **Objective:** predict continuous protein stability change
- **Metrics:** RMSE and Pearson correlation

We compare two modeling approaches:

1. **Tabular baselines**  
   Models using mutation-level physicochemical features and experimental condition features.

2. **Graph neural networks**  
   Models trained on protein residue contact graphs, where nodes represent amino acids and edges represent sequence or structural contacts.

Our original hypothesis was that residue contact graphs would improve protein-level ΔΔG prediction by giving the model access to spatial structural context. The final result is more nuanced: the strongest full-test model is a condition-aware HistGradientBoosting tabular model, while GNN ablations reveal where graph topology helps, especially for buried residues with dense contact neighborhoods.

## Main Files

### `index.html`

The final HTML blog website. This is the main project deliverable.

### `01_data_exploration_xgboost_baseline.ipynb`

Builds the initial XGBoost prototype on the smaller UniProt-annotated subset. This notebook includes data exploration, feature construction, XGBoost training, and comparison of per-mutation versus protein-level splits.

### `02_gnn_final_model.ipynb`

Trains and evaluates the final GNN variants and tabular baselines on the larger cleaned dataset. This notebook saves model comparison tables, seed-level GNN results, prediction files, ASA-stratified analyses, training histories, and graph coverage summaries.

### `03_reproduce_blog_figures.ipynb`

The main reproducibility notebook. It loads saved CSV/JSON outputs and regenerates the figures used in `index.html`.

### `04_protein_visualization.ipynb`

Generates local protein visualization assets, including the residue contact graph viewer and the side-by-side wild-type versus mutant protein structure viewer.

## Repository Structure

```text
aml-final-project/
├── index.html
├── README.md
├── single_point_mutations.tsv
│
├── 01_data_exploration_xgboost_baseline.ipynb
├── 02_gnn_final_model.ipynb
├── 03_reproduce_blog_figures.ipynb
├── 04_protein_visualization.ipynb
│
├── assets/
│   ├── figures/
│   │   └── final blog-ready figures and tables
│   ├── js/
│   │   └── 3Dmol-min.js
│   ├── contact_graph_example_final_main.json
│   ├── structure_viewer.html
│   └── structure_viewer_pair.html
│
├── results/
│   ├── xgboost/
│   ├── all_predictions_final_main.csv
│   ├── all_predictions_with_context_final_main.csv
│   ├── asa_stratified_results_final_main.csv
│   ├── baseline_results_final_main.csv
│   ├── cleaned_data_with_splits_final_main.csv
│   ├── gnn_seed_results_final_main.csv
│   ├── gnn_summary_results_final_main.csv
│   ├── graph_coverage_final_main.csv
│   ├── label_distribution_final_main.csv
│   ├── model_comparison_final_main.csv
│   ├── model_ranking_final_main.csv
│   ├── tabular_results_final_main.csv
│   ├── training_history_final_main.csv
│   ├── v4_seed_results_final_main.csv
│   └── v4_summary_results_final_main.csv
│
└── structure_visualization_cache/
    └── pdb_files/
```

## Python Requirements

## Python Requirements

The HTML blog itself does not require Python. It only requires opening `index.html` in Chrome.

To run the figure reproduction notebook:

```bash
pip install numpy pandas matplotlib seaborn scipy scikit-learn
```

## Model Variants

The final GNN notebook evaluates four GNN variants:

- **V1:** local mutation-site graph embedding only
- **V2:** local graph embedding plus pH and temperature condition features
- **V3:** local graph embedding plus global graph pooling plus condition features
- **V4:** structure-only GNN evaluated on structure-backed examples only

V4 is not strictly comparable with V1–V3 because it uses a smaller subset of examples with real structure-backed graphs.

## Saved Outputs

The final blog and figure reproduction notebook rely on saved outputs in:

```text
results/
```

and XGBoost-specific outputs in:

```text
results/xgboost/
```

These files allow the final figures to be regenerated without rerunning expensive model training.

## Interactive Structure Viewers

The website includes local interactive visualizations:

```text
assets/structure_viewer.html
assets/structure_viewer_pair.html
```

These use a local vendored copy of:

```text
assets/js/3Dmol-min.js
```

The side-by-side protein viewer shows the Cytochrome b5 V45E example using embedded PDB coordinates, so it does not need to fetch structures from the internet at render time.
