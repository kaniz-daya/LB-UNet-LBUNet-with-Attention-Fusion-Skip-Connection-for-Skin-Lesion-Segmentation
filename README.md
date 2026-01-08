# LB-UNet-LBUNet-with-Attention-Fusion-Skip-Connection-for-Skin-Lesion-Segmentation

🧩 Problem Statement

Accurate skin lesion segmentation is critical for early melanoma detection. While LB-UNet achieves strong boundary-aware segmentation, it relies on:

Handcrafted skip-fusion rules

Multiple auxiliary supervision branches

Higher computational overhead

This project investigates whether a simpler, attention-based fusion strategy can:

Reduce architectural complexity

Improve inference speed

Retain competitive segmentation accuracy

🧠 Proposed Approach

We introduce Attention Skip Fusion (ASF), a learnable module that adaptively fuses encoder and decoder features at each skip connection.

Key Modifications

Replace handcrafted fusion with AttentionSkipFusion

Remove auxiliary prediction branches

Simplify decoder structure

Use a stabilized BCE + Dice loss

Retain full-depth encoder–decoder in final model

🏗️ Architecture Overview

Encoder–decoder U-Net style network

Feature dimensions: [8, 16, 24, 32, 48, 64]

AttentionSkipFusion applied at all skip connections

Transposed convolutions for upsampling

Final sigmoid output for binary segmentation

📊 Dataset

ISIC 2018 Skin Lesion Segmentation Dataset

RGB dermoscopic images + binary masks

Split into train / validation / test

Images resized to 256 × 256

⚙️ Training Details

Framework: PyTorch

Optimizer: AdamW

Learning Rate: 1e-3

Scheduler: CosineAnnealingLR

Batch Size: 8

Epochs: 300

Predictions are clamped to avoid numerical instability.

📈 Evaluation Metrics

Mean Intersection over Union (mIoU)

Dice Similarity Coefficient (DSC / F1-score)

Pixel Accuracy

Sensitivity & Specificity

🏆 Results Summary
Model	Val mIoU	Val DSC	Test mIoU	Test DSC
Original LB-UNet	0.7922	0.8731	0.8111	0.8899
Modified LB-UNet (ASF)	0.7884	0.8706	0.8043	0.8824
⏱️ Efficiency

Inference speed improved by ~40%

808 test images processed in ~7 seconds vs ~12 seconds

🔍 Key Insights

Attention-based fusion improves architectural simplicity

Removal of deep supervision causes slight performance degradation

ASF alone cannot fully replace boundary-aware auxiliary learning

Strong candidate for real-time or resource-constrained deployment

📂 Recommended Repository Structure
lb-unet-attention/
│
├── data/
│   ├── train/
│   ├── val/
│   ├── test/
│
├── models/
│   ├── lbunet.py
│   ├── attention_skip_fusion.py
│
├── training/
│   ├── train.py
│   ├── loss.py
│
├── results/
│   ├── metrics.csv
│   ├── predictions/
│
├── README.md
└── requirements.txt

🧾 Resume-Ready Description

Skin Lesion Segmentation Using Attention-Based LB-UNet
Designed and evaluated a lightweight modification of LB-UNet by introducing learnable attention-based skip connections. Achieved ~40% faster inference on ISIC 2018 dataset with minimal reduction in segmentation accuracy (mIoU 0.804). Implemented in PyTorch with BCE–Dice loss and extensive ablation studies.

🧪 Technologies Used

Python

PyTorch

NumPy, OpenCV

TensorBoard

Medical Image Processing

👩‍💻 Authors

Kaniz Fatima Daya
Muhammed Nazmul Arefin

King Fahd University of Petroleum and Minerals (KFUPM)

Supervisor: Dr. Abdul Jabbar Siddiqui

📌 Future Work

Hybrid attention + boundary supervision

Transformer-based skip connections

Knowledge distillation from full LB-UNet

Multi-class lesion segmentation

3D medical image extension
