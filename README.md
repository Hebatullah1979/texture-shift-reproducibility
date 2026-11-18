
Compact Wavelet–Binary Texture Descriptors under Acquisition and Specimen Shift — reproducibility package
Code, partitions, and predictions for the article Compact Wavelet–Binary Texture Descriptors under Acquisition and Specimen Shift: A Reproducible Comparative Study by Hebatullah Khattab and Amer Abu Salem (Zarqa University), International Journal of Advanced Computer Science and Applications (IJACSA), 2026.

Contents
Path	Description
experiment.py	Feature extraction (Haar DWT, LBP) and nested SVM evaluation with the original grid (gamma = 1, C in {0.1, 1, 10}).
audit.py	Checks invariants and train/test separation of every recorded partition.
results/	Image manifests with SHA-256 hashes, archive checksums, cached features (kth1_features.npz, kth2_features.npz), all outer and inner partitions (*_splits.json), all original-grid predictions (*_records.json, all_records.json), summaries, timings, and dependency versions.
revision/revision_analysis.py	Grid sensitivity analysis (original, extended, widest grid) and fold-level / class-by-fold paired analyses.
revision/clbp_baseline.py	Completed LBP (CLBP_S/M/C) baseline with identical sampling and nested evaluation.
revision/results_revision/	All revision outputs: per-fold records with predictions and selected hyperparameters for every grid (multi_records.json, clbp_results_wide.json), summaries, paired analyses (variance_*.json), and CLBP feature caches (clbp_kth*.npy, float32, manifest order).
Data
The KTH-TIPS and KTH-TIPS2b images are distributed by KTH and are not included: https://www.csc.kth.se/cvap/databases/kth-tips/download.html

Place kth_tips_grey_200x200.tar and kth-tips2-b_col_200x200.tar in data/. Their SHA-256 checksums are in results/archive_hashes.json. The cached features in results/ and revision/results_revision/ allow every classifier experiment to be rerun without the images.

Reproduce
Python with numpy, scipy, scikit-learn, Pillow, and matplotlib (versions in requirements.txt and results/versions.json).

python experiment.py                                   # original-grid experiments (needs data/)
python audit.py                                        # partition and invariant checks
python revision/revision_analysis.py results multi     # three nested grids, all six fusion/wavelet/LBP configurations
python revision/revision_analysis.py results variance  # paired analyses on the original-grid records
python revision/clbp_baseline.py results <kth1-image-dir> <kth2-image-dir>   # CLBP baseline (needs extracted images)
Verification performed
revision_analysis.py repro reproduces all published original-grid values exactly; the multi pass reproduces them to within 0.03 percentage points (floating-point tie-breaking).
The precomputed RBF kernel used in the revision gives 100% prediction agreement with SVC(kernel='rbf').
For all 5,562 images, the CLBP joint histogram summed over its magnitude and center components equals the LBP histogram (maximum deviation 1.7e-16).
Contact
Hebatullah Khattab (h.awwad@zu.edu.jo), Amer Abu Salem (abusalem@zu.edu.jo) Department of Computer Science, Faculty of Information Technology, Zarqa University, Zarqa, Jordan

