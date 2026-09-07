
# Bagged-Projected Isolation Forest (BP-IF)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/fzaman3g-cloud/BP-IF/blob/main/BP_IF_Reproducibility_M50_T10.ipynb)

Official implementation of **BP-IF: Bagged-Projected Isolation Forest for Robust Anomaly Detection**, accepted at the 33rd International Conference on Neural Information Processing (ICONIP 2026) and to appear in Springer's Communications in Computer and Information Science (CCIS) series.

BP-IF combines bootstrap sampling and Gaussian random projection to create diverse sample- and representation-level views. An Isolation Forest is trained on each projected view, and the branch-level anomaly scores are averaged to obtain the final anomaly score.

## Authors

- Fahad Zaman Chowdhury
- Md Geaur Rahman
- Md Zahidul Islam

Charles Sturt University, Australia.

## Repository contents

```text
BP-IF/
├── BP_IF_Reproducibility_M50_T10.ipynb
├── BP-IF Figures/
├── .gitignore
├── LICENSE
└── README.md
```

The notebook contains:

1. the BP-IF implementation and main evaluation;
2. controlled anomaly-ratio analysis at 1%, 3%, and 5%;
3. ablation analysis of the complete method and its components; and
4. Friedman tests using the dataset-level results reported in the paper.

Implementations of the comparison methods are not included.

## Requirements

The notebook is designed for Google Colab and uses the following Python packages, which are available in the standard Colab environment:

- NumPy
- pandas
- SciPy
- scikit-learn
- IPython

No GPU is required.

## Datasets

The paper evaluates BP-IF on five publicly available anomaly-detection datasets:

- Backdoor
- Cardio
- Census
- Cover
- MNIST

These benchmark datasets are available through the [ADBench dataset collection](https://github.com/Minqi824/ADBench). Dataset files are not redistributed in this repository and remain subject to their original licences and terms of use.

The notebook accepts one prepared CSV file at a time. The CSV must contain numeric feature columns and one binary label column using the following convention:

- `0`: normal
- `1`: anomaly

Common label-column names are detected automatically. Otherwise, set `LABEL_COLUMN` in the **Dataset input** cell. For categorical labels, set `BENIGN_LABEL` to the value representing normal observations. Rows containing non-finite numeric feature values are excluded.

## BP-IF configuration

| Parameter | Description | Value |
|---|---|---:|
| $M$ | Bootstrap-projection branches | 50 |
| $T$ | Isolation trees per branch | 10 |
| $\alpha$ | Bootstrap sampling ratio | 0.7 |
| $k$ | Configured projection dimension | 32 |
| $\psi$ | Isolation Forest subsample size | 256 |
| Aggregation | Branch-level score aggregation | Mean |

The implementation sets the effective projection dimension to $\min(32,d)$, where $d$ is the number of input features. The main evaluation uses a stratified 75/25 train-test split, 10 runs, and seeds 42--51. Standardization is fitted only on each training partition and then applied to its corresponding test partition.

## Running the notebook

1. Click the **Open in Colab** badge at the top of this page.
2. Run the cells sequentially.
3. When prompted by the **Dataset input** cell, upload a prepared CSV file.
4. If automatic label detection fails, set `LABEL_COLUMN` to the exact column name and rerun the cell.
5. Run the main evaluation and any additional analysis cells required.

The complete notebook performs several repeated ensemble experiments and may require substantial execution time on large datasets.

## Outputs

The main experiment reports mean and standard deviation across repeated runs for:

- AUC-ROC;
- AUC-PR;
- preprocessing time;
- projection time;
- training time;
- testing time; and
- total runtime.

The principal output variables are:

```text
bpif_summary
bpif_all_runs
bpif_ratio_summary
bpif_ratio_all_runs
ablation_summary
ablation_all_runs
friedman_results
```

The anomaly-ratio and ablation cells calculate results for the uploaded dataset. The Friedman cell uses the fixed dataset-level results reported in the paper and is independent of the uploaded dataset.

## Reproducibility notes

- Random seeds and model parameters are explicitly defined in the notebook.
- Standardization uses training data only.
- The dataset labels are used for evaluation and stratified splitting, not for fitting BP-IF.
- Source datasets, comparison methods, and third-party packages remain subject to their respective licences.
- Runtime can vary across hardware and software environments.

## Citation

Please cite the following paper when using this implementation:

```bibtex
@inproceedings{chowdhury2026bpif,
  title     = {BP-IF: Bagged-Projected Isolation Forest for Robust Anomaly Detection},
  author    = {Chowdhury, Fahad Zaman and Rahman, Md Geaur and Islam, Md Zahidul},
  booktitle = {Proceedings of the 33rd International Conference on Neural Information Processing},
  year      = {2026},
  publisher = {Springer}
}
```

The entry will be updated with the final CCIS volume, page range, editors, and DOI when the bibliographic record becomes available.

## Licence

The original BP-IF code is released under the [MIT License](LICENSE). Dataset and third-party software licences apply separately.

## Contact

**Fahad Zaman Chowdhury**  
Charles Sturt University  
Email: fchowdhury@csu.edu.au
