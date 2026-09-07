

# Bagged-Projected Isolation Forest (BP-IF)

Official implementation of **BP-IF: Bagged-Projected Isolation Forest for Robust Anomaly Detection**, accepted at the 33rd International Conference on Neural Information Processing (ICONIP 2026) and to appear in Springer Communications in Computer and Information Science (CCIS).

BP-IF combines bootstrap sampling and Gaussian random projection to create diverse sample- and representation-level views. An Isolation Forest is trained on each projected view, and the branch-level anomaly scores are averaged to obtain the final anomaly score.

## Authors

- Fahad Zaman Chowdhury
- Md Geaur Rahman
- Md Zahidul Islam

Charles Sturt University, Australia.

## Repository contents

The repository provides the BP-IF implementation, experimental code, parameter settings, dataset preparation instructions, and outputs required to reproduce the results reported in the paper.

```text
BP-IF/
├── README.md
├── LICENSE
├── requirements.txt
├── code/ or notebooks/
├── datasets/
└── results/
```

The precise directory names may be adjusted to match the uploaded files.

## Installation

Clone the repository and install the required Python packages:

```bash
git clone https://github.com/fzaman3g-cloud/BP-IF.git
cd BP-IF
pip install -r requirements.txt
```

The experiments were implemented in Python. Exact package versions should be recorded in `requirements.txt`.

## Datasets

The experiments use publicly available benchmark datasets reported in the paper. Dataset files are not redistributed in this repository. Download each dataset from its original source and follow the preparation instructions supplied with the experimental code.

Before running the experiments, place the prepared files in the following directory unless the code specifies another location:

```text
datasets/
```

For every dataset, preserve the label convention used in the paper:

- `0`: normal
- `1`: anomaly

Update this section with the five dataset names, source links, expected filenames, and any dataset-specific preprocessing steps before publishing the repository.

## Experimental configuration

The principal BP-IF configuration used in the paper is:

| Parameter | Description | Value |
|---|---|---:|
| $M$ | Bootstrap–projection branches | 50 |
| $T$ | Isolation trees per branch | 10 |
| $\alpha$ | Bootstrap sampling ratio | 0.7 |
| $k$ | Gaussian random-projection dimension | 32 |
| $\psi$ | Isolation Forest subsample size | 256 |
| Aggregation | Branch-level score aggregation | Mean |

The baseline configurations are:

- **IF:** 100 trees and subsample size $\psi=256$.
- **EIF:** 100 trees and subsample size $\psi=256$.
- **DIF:** $i=3$, $M=50$, and $T=6$, following its default configuration.
- **Additional fairness check:** IF with 500 trees.

All random seeds, preprocessing operations, and train/test settings should remain fixed as specified in the experimental code.

## Running the experiments

If the implementation is provided as a Jupyter notebook, open the principal experiment notebook and run all cells sequentially:

```bash
jupyter notebook
```

Then select **Kernel → Restart Kernel and Run All Cells**.

If executable scripts are provided, document the exact reproduction command here, for example:

```bash
python experiments/run_all_experiments.py
```

Replace the example command with the actual command used by this repository before publication.

## Evaluation

The experiments report:

- AUC-ROC;
- AUC-PR; and
- runtime.

Repeated experiments should use the random seeds reported in the code. Generated result files should be saved under `results/` and compared with the paper's reported tables.

## Reproducibility checklist

Before creating the camera-ready release, verify that:

- a fresh clone runs without private or absolute file paths;
- `requirements.txt` contains the required package versions;
- dataset sources and preprocessing steps are documented;
- all random seeds and parameter settings are explicit;
- no passwords, tokens, or private data are included; and
- the generated AUC-ROC, AUC-PR, and runtime outputs correspond to the reported experiments.

## Citation

If you use this implementation, please cite:

```bibtex
@inproceedings{chowdhury2026bpif,
  title     = {BP-IF: Bagged-Projected Isolation Forest for Robust Anomaly Detection},
  author    = {Chowdhury, Fahad Zaman and Rahman, Md Geaur and Islam, Md Zahidul},
  booktitle = {Proceedings of the 33rd International Conference on Neural Information Processing},
  year      = {2026},
  publisher = {Springer}
}
```

Replace or extend this entry with the final CCIS volume, page range, editors, and DOI after Springer publishes the bibliographic record.

## Licence

The original BP-IF code is released under the MIT License. Third-party libraries, baseline implementations, and datasets remain subject to their respective licences and terms of use.

## Contact

For questions about the implementation, contact:

**Fahad Zaman Chowdhury**  
Charles Sturt University  
Email: fchowdhury@csu.edu.au
