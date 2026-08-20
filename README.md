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

The synthetic images contain randomly generated target regions represented using elliptical shapes over a noisy grayscale background.

## Preprocessing

The images are:

1. Resized to 128 × 128 pixels.
2. Converted to floating-point values.
3. Scaled from [0, 255] to [0, 1].
4. Normalized using mean = 0.5 and standard deviation = 0.5.

The corresponding masks are converted into binary segmentation masks.

## Model Architecture

A lightweight U-Net architecture, named `UNetMini`, is used.

The encoder contains convolutional blocks with:

- 32 channels
- 64 channels
- 128 channels

The bottleneck contains 256 channels.

The decoder progressively reconstructs the spatial resolution using transposed convolutions and skip connections.

The final 1×1 convolution produces a single-channel segmentation output.

### Architecture

Input (1 × 128 × 128)

→ Double Convolution (32)

→ Max Pooling

→ Double Convolution (64)

→ Max Pooling

→ Double Convolution (128)

→ Max Pooling

→ Bottleneck (256)

→ Decoder with Skip Connections

→ 1×1 Convolution

→ Output Segmentation Mask

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

Additional inference techniques explored in the project include:

- Probability threshold optimization
- Test-Time Augmentation (TTA)
- Connected-component post-processing
- Morphological post-processing

Visual overlays were generated to compare ground-truth regions and predicted regions.

## Results

The trained model produced segmentation predictions for the test dataset and generated visual overlays and a demonstration GIF.

A detailed numerical evaluation and visual outputs are available in the project notebook.

## Repository Contents

```text
flood-segmentation-cnn/
│
├── README.md
├── flood_segmentation.ipynb
└── best_model.pth

## Technologies Used
- Python
- PyTorch
- NumPy
- OpenCV
- Matplotlib
- ImageIO
- Google Colab
- CUDA
- GitHub

## How to Run

The project notebook can be opened in Google Colab or another compatible Jupyter environment.

The notebook contains the complete workflow including:

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
