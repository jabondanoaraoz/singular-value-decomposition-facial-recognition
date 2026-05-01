# SVD-Based Facial Recognition: Eigenfaces & Dimensionality Reduction

Unsupervised dimensionality reduction via Singular Value Decomposition (SVD) applied to the
[Labeled Faces in the Wild](https://www.aiaaic.org/aiaaic-repository/ai-algorithmic-and-automation-incidents/labeled-faces-in-the-wild-lfw-dataset) (LFW) dataset. The project
demonstrates eigenfaces for facial representation and SVD-projected features for binary
classification, with cross-validated hyperparameter tuning.

## Key Results

| Model | K | Recall | Precision | F1 | AUC |
|---|---|---|---|---|---|
| Baseline | 1,000 | 0.684 | 0.578 | 0.626 | 0.862 |
| CV-tuned | **200** | **0.714** | 0.648 | 0.680 | 0.902 |

Cross-validation identified K=200 as optimal, using 5x fewer features than the baseline, with
~3 percentage points gain in recall and improved performance across all metrics.

## Project Structure

```
.
├── svd_eigenfaces.ipynb   # Main notebook
├── requirements.txt
└── data/                  # LFW images (auto-downloaded on first run, gitignored)
```

Images generated during notebook execution are saved to `images/` (gitignored).

## Setup

```bash
pip install -r requirements.txt
jupyter notebook svd_eigenfaces.ipynb
```

Run all cells in order. The LFW dataset (~200 MB) is downloaded automatically via
scikit-learn on the first run.

## Methodology

1. **Mean subtraction**: centers the data matrix before decomposition.
2. **Full SVD**: decomposes the centered matrix; right singular vectors are the eigenfaces.
3. **Scree plot**: shows cumulative variance explained vs K to justify truncation choice.
4. **Leakage-free protocol**: SVD and mean centering computed on training data only;
   test set projected onto training-derived basis vectors.
5. **5-fold stratified CV**: SVD re-computed within each fold; K selected to maximize
   recall on the positive class (George W. Bush).

## References

- Sirovich & Kirby (1987). *A low-dimensional procedure for the characterization of human faces.* JOSAA.
- Turk & Pentland (1991). *Eigenfaces for recognition.* Journal of Cognitive Neuroscience.
- Huang et al. (2007). *Labeled Faces in the Wild.* UMass Technical Report 07-49.

---

## Academic Context

This project was developed as part of the **Master's in Analytical Intelligence of Data (MIAD)** program at Universidad de los Andes, Colombia.

---

## Autor

**Joaquín Abondano Araoz** - Data Analytics · AI & Automation · Strategic Planning

[Website](https://joaquinabondano.com) · [LinkedIn](https://linkedin.com/in/joaquin-abondano) · [GitHub](https://github.com/jabondanoaraoz)
