# Flood Region Segmentation Using CNN

## Project Overview

This project implements a CNN-based flood region segmentation system using a lightweight U-Net architecture. The model processes grayscale images and predicts pixel-level flood regions using corresponding ground-truth masks.

The project was developed as part of the Summer Training Programme on Data Science, Machine Learning & Agentic AI organised by the Electronics & ICT Academy, IIT Roorkee.

## Problem Statement

Flooded regions in images need to be identified automatically for effective image-based analysis. Traditional manual identification can be time-consuming. This project explores a deep-learning-based approach to automatically identify target flood regions at the pixel level.

## Objective

The main objectives are:

- Generate and work with a synthetic flood-image dataset.
- Develop a CNN-based segmentation model.
- Train the model using ground-truth segmentation masks.
- Evaluate segmentation performance using Intersection over Union (IoU).
- Apply thresholding, test-time augmentation and post-processing.
- Export the trained model for further use.

## Dataset

A synthetic dataset was generated using Python, NumPy and OpenCV.

| Split | Images |
|---|---:|
| Training | 200 |
| Validation | 40 |
| Testing | 40 |
| **Total** | **280** |

Image properties:

- Image size: 128 × 128 pixels
- Image type: Grayscale
- Input channels: 1
- Ground-truth masks: Binary
- Training batch size: 16

## Preprocessing

The images are resized to 128 × 128 pixels, converted to floating-point values, scaled to [0,1], and normalized using mean = 0.5 and standard deviation = 0.5.

The corresponding masks are converted into binary segmentation masks.

## Model Architecture

A lightweight U-Net architecture, named `UNetMini`, is used.

The encoder contains convolutional blocks with 32, 64 and 128 channels. The bottleneck contains 256 channels. The decoder uses transposed convolutions and skip connections to reconstruct the segmentation output.

The final 1×1 convolution produces a single-channel segmentation mask.

## Training

The model was trained using:

- Optimizer: AdamW
- Learning rate: 0.001
- Weight decay: 0.0001
- Epochs: 6
- Batch size: 16
- Training device: CUDA/GPU

A combined Binary Cross-Entropy and Dice loss was used:

**Combined Loss = 0.5 × BCE + 0.5 × Dice Loss**

## Evaluation

Intersection over Union (IoU) was used to evaluate segmentation performance.

Additional inference techniques explored include:

- Probability threshold optimization
- Test-Time Augmentation (TTA)
- Connected-component post-processing
- Morphological post-processing

The project also generates visual overlays comparing ground-truth and predicted regions.

## Results

The trained model successfully produced segmentation predictions on the test dataset. The project generated prediction overlays and demonstration visualizations for qualitative evaluation.

The detailed results are available in the project notebook.

## Repository Contents

```text
flood-segmentation-cnn/
├── README.md
├── flood_segmentation.ipynb
├── best_model.pth
├── model.onnx
└── requirements.txt

```
## Technologies Used

- Python
- PyTorch
- NumPy
- OpenCV
- Matplotlib
- ImageIO
- Google Colab
- CUDA
- ONNX
- GitHub

## How to Run

Open `flood_segmentation.ipynb` in Google Colab or another compatible Jupyter environment.

The notebook contains the complete workflow:

1. Synthetic dataset generation
2. Dataset preprocessing
3. CNN/U-Net model definition
4. Model training
5. Validation
6. Test inference
7. IoU evaluation
8. Prediction visualization
9. Post-processing

## Future Scope

The project can be extended by:

- Using real satellite or remote-sensing flood datasets.
- Increasing dataset size and diversity.
- Experimenting with larger segmentation architectures.
- Applying advanced augmentation techniques.
- Improving generalization to real-world flood imagery.
- Deploying the trained model as a web or desktop application.

## Project Author

**Apoorva**

Developed as part of the Summer Training Programme on Data Science, Machine Learning & Agentic AI organised by Electronics & ICT Academy, IIT Roorkee.
