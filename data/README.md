# Dataset

Place your authorized CoNLL files here as `train_clean.txt`, `val_clean.txt`, and `test_clean.txt`.
The notebook reads the first column as the token and the last column as its label.
Blank lines separate sequences. Labels are `B-FP`, `I-FP`, and `O`.

`example.conll` is a synthetic format illustration only. It cannot reproduce research results.
The uploaded research corpus is not redistributed in this package. Record the dataset version, article-level split procedure, checksums, annotation rules, and availability statement when releasing the corpus.

The project's constraints require feature entities to contain at least two words.
