## Effect of Dimensionality Reduction (KNN on Medical Data)

This repo compares k‑nearest neighbors performance before and after feature selection on two medical datasets (`heart 2.csv`, `o2Saturation.csv`). The notebooks explore forward and backward sequential feature selection as well as random-forest-based selection to quantify how much accuracy is lost or gained when reducing dimensionality.

### Repo layout
- `heart_knn_*.ipynb`: experiments on the heart disease dataset.
- `knn_*.ipynb`: experiments on the oximetry/saturation dataset.
- `*.csv`: source data.
- `Accuracy Metrics.png`: saved chart from one of the runs.

### Quick start
1. Create an environment with Python 3.8+.
2. Install dependencies: `pip install numpy pandas seaborn matplotlib scikit-learn mlxtend`.
3. Open any notebook in Jupyter or VS Code and run all cells.

### Key findings
- **Heart dataset**
  - Baseline (no reduction): test accuracy ≈ **0.859**.
  - Forward selection: best test accuracy ≈ **0.859** (at ~20 features) — essentially tied with the baseline.
  - Backward elimination: test accuracy ≈ **0.840**, a small drop versus baseline.
  - Random-forest-selected features: test accuracy ≈ **0.864**, the best of the heart runs with slight gain over the full feature set.
- **Oximetry dataset**
  - Baseline (no reduction): test accuracy ≈ **0.969**.
  - Forward selection: test accuracy ≈ **0.943**, showing the biggest drop.
  - Backward elimination: best test accuracy ≈ **0.978** (at ~24–27 features), a modest improvement over baseline.
  - Random-forest-selected features: test accuracy ≈ **0.974**, slightly better than baseline.

### Interpretation
- Light feature pruning generally preserves accuracy; aggressive forward selection can hurt when informative variables are removed.
- Backward elimination recovered equal or better accuracy on the oximetry data, suggesting redundancy the model could drop, while the heart data was more sensitive to removal.
- Tree-based importance (random forest) offered the safest reduction path here, giving small gains without full dimensionality.

### Repro notes
- Numbers above are taken from the printed `Train/Test set Accuracy` lines inside the notebooks.
- Randomness comes from train/test splits; set a fixed seed in the notebooks if you want bit-for-bit reproducibility.
