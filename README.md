# Cell Segmentation with U-Net (Kaggle Competition)
Project Overview
This project implements a custom U-Net architecture in PyTorch to perform cell segmentation on microscopy images for a Kaggle competition. The end goal is to minimize the mean absolute error (MAE) in counting segmented cells. All code and model development were done from scratch, following best ML engineering practices.

Technical Workflow
1. Data Preparation & Visualization
Loaded .npz training dataset (X, y) provided by the competition.

Visualized image-mask pairs for sanity check.

2. Custom Dataset & DataLoader
Created a CellDataset PyTorch class for images and masks.

Split dataset (train/validation, 80/20) with train_test_split.

Used DataLoader with batch processing.

3. U-Net Architecture (from scratch)
Implemented a flexible U-Net in PyTorch:

Encoder: 5-levels, double conv, batch norm, ReLU, max-pooling.

Decoder: transposed convolution upsampling, skip connections, output head.

Modular CC (convolutional block) for code reuse and easier tuning.

4. Training Pipeline & Experiments
Loss: BCEWithLogitsLoss for binary mask regression.

Optimizer: Adam (experimented with different learning rates).

Epochs: Early experiments with 30 epochs, later extended to 100 epochs + early stopping.

Early Stopping: Monitored validation loss, stopped if no improvement for 10 epochs, saving the best model.

Hardware: Automatic use of GPU if available.

5. Training Diagnostics
For each experiment, plotted training/validation loss curves vs. epochs for convergence analysis.

Used the plots to diagnose overfitting and guide early stopping.

6. Post-processing & Validation Scoring
Applied thresholding and morphological post-processing to model outputs.

Grid searched over sigmoid thresholds (r) and minimum object size (min_size) for best MAE on validation set.

Used skimage for connected component labeling and object removal.

7. Results & Submission
Achieved final validation MAE < 3 (meeting competition requirements).

Saved segmented masks for qualitative inspection.

Final model and parameters used to generate Kaggle submission file.
