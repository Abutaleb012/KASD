# Kernel Adaptive Subspace Detector (KASD) for Hyperspectral Imagery

Python implementation of the linear adaptive subspace detector (ASD) and its kernel version (KASD), tested first on synthetic data and then on a hyperspectral oil-spill scene.

Part of the PhD research of **Ali Abutaleb, PhD** (George Mason University, 2023):
*Integrating Nonlinear Kernel-Based Detector Algorithms and Minimum Noise Fraction for Advanced Oil-Spill Detection with Hyperspectral Imagery.*

Portfolio: [abutaleb012.github.io](https://abutaleb012.github.io/) · Write-up: [How I found oil spills in hyperspectral imagery](https://abutaleb012.github.io/oil-spill/)

## Method

1. **Synthetic test.** Two toy datasets of 300 points: (A) a Gaussian mixture and (B) a nonlinearly mapped version of it. ASD and KASD decision boundaries are plotted for both, to show where a linear detector breaks.
2. **Real data.** A hyperspectral flight line of 26,159 × 796 pixels with 224 bands, and a 285 × 76 pixel region of interest with a labeled oil ground truth.
3. **Representative pixels.** K-means selects 300 background and 300 target centroids for the kernel matrices.
4. **Detectors.** Linear ASD, then KASD with Gaussian RBF, polynomial, and spectral angle kernels.
5. **Evaluation.** Accuracy, precision, recall, F1 score, and ROC curves.

## Results on the oil-spill region

| Detector | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| Linear ASD | 0.94 | 0.40 | 0.13 | 0.20 |
| KASD, Gaussian RBF | 0.97 | 0.65 | 0.31 | 0.42 |
| KASD, polynomial | 0.95 | 0.98 | 0.29 | 0.44 |
| KASD, spectral angle | 0.93 | 0.06 | 0.02 | 0.03 |

The Gaussian and polynomial kernels roughly double the F1 score of the linear detector. Recall stays low on this small region, so this detector is the weakest of the four in the series; [KMSD](https://github.com/Abutaleb012/KMSD) and [KOSP](https://github.com/Abutaleb012/KOSP) perform best.

On the synthetic data, KASD with a Gaussian kernel reaches an F1 score of 0.94 on dataset A, where linear ASD reaches 0.73.

## Files

- `KASD.ipynb`: the full notebook (toy data, ASD, KASD, real data, ROC).

## Running it

The hyperspectral data is not included. Place both ENVI files in `./data/` and run the notebook top to bottom. Written for Python 3.7 with:

```
numpy  scipy  scikit-learn  spectral  sympy  matplotlib  pillow
```

## Related repositories

- [KOSP](https://github.com/Abutaleb012/KOSP): kernel orthogonal subspace projection
- [KMSD](https://github.com/Abutaleb012/KMSD): kernel matched subspace detector
- [KSMF](https://github.com/Abutaleb012/KSMF): kernel spectral matched filter
- [KASD_2021](https://github.com/Abutaleb012/KASD_2021): later version of this notebook

## Reference

H. Kwon and N. M. Nasrabadi, "Kernel adaptive subspace detector for hyperspectral imagery," *IEEE Geoscience and Remote Sensing Letters*, 2006.
