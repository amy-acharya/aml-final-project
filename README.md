# Fold or Fail: Predicting Protein Stability Changes from Mutations

This repository is for our Applied Machine Learning final project. 
We chose to investigate whether graph neural networks (GNNs) on protein residue contact graphs improve prediction of mutation-induced protein stability changes, measured as ΔΔG, beyond baselines like XGBoost.

## Project Overview

A single amino acid mutation can change how stable a protein is. Our task was to predict ΔΔG from single-point mutation data.

We compare two modeling approaches:

1. **Tabular baselines**  
   Models trained on mutation-level physicochemical and experimental features.

2. **Graph neural networks**  
   Models trained on protein residue graphs where nodes are amino acids and edges represent sequence or structural contacts.

Our driving question was if GNNs improve accuracy, and when graph structure becomes more useful for exploring structural relationships in protein data.

## Repository Structure
