# ELECTRA–BiLSTM–MMCRF for Forensic Software Feature Extraction

Research code for extracting forensic software feature phrases from English news articles using ELECTRA, a bidirectional LSTM, a custom masked conditional random field, and an auxiliary MoM token loss.

**Status:** notebook-based research snapshot. This repository packages the supplied implementation; it is not a validated reproduction of published results. Read [Known limitations](docs/KNOWN_LIMITATIONS.md) before using its metrics.

## Overview

The model assigns `B-FP`, `I-FP`, and `O` labels. Its transition constraints target feature phrases of at least two words. The encoder is `google/electra-base-discriminator`.

## Repository contents

| Path | Purpose |
| --- | --- |
| `notebooks/train_evaluate.ipynb` | Complete model, training, evaluation, and plotting workflow |
| `data/README.md` | Dataset format and local placement instructions |
| `data/example.conll` | Synthetic format example, not an experimental dataset |
| `models/` | Locally generated checkpoints |
| `results/` | Place exported experiment results here |
| `docs/KNOWN_LIMITATIONS.md` | Implementation issues that affect reproducibility |
| `docs/UPLOAD_GUIDE_ID.md` | GitHub upload instructions in Indonesian |
| `requirements.txt` | Direct Python dependencies; not a tested lockfile |

## Installation

Create a Python virtual environment, activate it, then install dependencies:

```bash
python -m venv .venv
# Windows PowerShell:
.venv\Scripts\Activate.ps1
# macOS/Linux instead: source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab
```

Install a CUDA-compatible PyTorch build if GPU training is required. The dependency list is intentionally unpinned because a verified training-environment lockfile was not supplied. After a successful run, capture the environment with `python -m pip freeze > requirements-lock.txt`.

## Data

Place the actual dataset splits at `data/train_clean.txt`, `data/val_clean.txt`, and `data/test_clean.txt`. Each line contains a token and its BIO label; blank lines separate sequences. The full research corpus is not bundled. See [data instructions](data/README.md).

## Run the experiment

1. Start Jupyter from this repository root.
2. Open `notebooks/train_evaluate.ipynb`.
3. Review the configuration cell and the model constructor call inside `main()`.
4. Run the cells in order. Dependencies should already be installed; the inherited pip-install cell may be skipped.
5. The notebook selects a checkpoint using validation partial entity F1, reloads it, and evaluates the test split. Charts are displayed inline; export them manually if needed.

Do not select hyperparameters using test results. Save the effective configuration and environment alongside each new run.

## Effective settings in this snapshot

| Setting | Value |
| --- | --- |
| Encoder | `google/electra-base-discriminator` |
| Maximum sequence length | 256 subtokens, including special tokens |
| Batch size / maximum epochs / seed | 8 / 15 / 42 |
| Actual LSTM hidden size | 256 per direction (512 concatenated) |
| LSTM layers / dropout | 2 / 0.3 |
| Encoder / head learning rate | 2e-5 / 2e-3 |
| Effective transition penalty | 100 |
| MoM coefficient / easy-O threshold | 1.5 / 0.99 |
| Early stopping | Validation partial F1, patience 5, min_delta 1e-4 |

The notebook's `LSTM_HIDDEN = 128` variable is unused by the constructor call. The actual model uses its default of 256. This discrepancy is preserved and documented rather than silently changing the experiment.

## Evaluation and results

The supplied notebook reports token macro F1, partial entity scores, exact entity scores, and transition plots. Entity evaluation and transition counts currently operate on flattened sequences; these are known limitations. No new training or numerical results are claimed by this packaging release.

## Method reference

Wei, T., Qi, J., He, S., and Sun, S. (2021). [Masked Conditional Random Fields for Sequence Labeling](https://aclanthology.org/2021.naacl-main.163/). NAACL-HLT, 2024–2035. [Authors' implementation](https://github.com/DandyQi/MaskedCRF).

This project is a custom implementation with additional constraints and MoM loss, not the authors' official code. Publication title, DOI, author list, and a software license should be added by the project owner when confirmed. No publication or license status is asserted here.
