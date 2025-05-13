# Adversarial Attacks on Deep Models

## Project Overview

This repository explores the vulnerability of state-of-the-art image classifiers to both pixel-wise and localized patch-based adversarial attacks. We focus on four pretrained models:

- **ResNet-34** (21.8 M parameters)  
- **SqueezeNet1_0** (1.2 M parameters)  
- **ViT-B_16** (86.6 M parameters)  
- **Swin-V2** (28.4 M parameters)  

Our goal is to quantify how small, imperceptible perturbations can drastically reduce model accuracy, and how architectural differences (depth, parameter count, convolution vs. attention, hierarchical structure) affect robustness.

## Attack Methods

1. **FGSM** (Fast Gradient Sign Method)  
2. **I-FGSM** (Iterative FGSM)  
3. **MI-FGSM** (Momentum Iterative FGSM)  
4. **PGD** (Projected Gradient Descent with restarts)  
5. **Patch-PGD** (32×32 localized patch with Nesterov momentum)

Each attack is applied under a fixed ℓ∞‐norm budget, and we record both Top-1 and Top-5 accuracy drops.

## Key Findings

- **ResNet-34**:  
  - FGSM (ε=0.02) plunges Top-1 from 76% → 6.2%.  
  - Iterative attacks (I-FGSM, MI-FGSM, PGD) drive Top-1 to ~0%.  
  - Patch-PGD still retains ~12% Top-1, showing some resilience to localized perturbations.

- **SqueezeNet1_0**:  
  - Extremely fragile: all pixel-wise attacks collapse Top-1 to 0%.  
  - Patch-PGD only recovers ~2% Top-1.

- **ViT-B_16**:  
  - FGSM drops Top-1 from 82.5% → 45.4%.  
  - Iterative attacks reduce Top-1 to single digits; Patch-PGD retains ~23% Top-1.

- **Swin-V2**:  
  - FGSM reduces Top-1 to ~28%; iterative attacks again collapse to near 0%.  
  - Patch-PGD retains ~24% Top-1, reflecting its hierarchical windowed attention.

- **Parameter Trend**:  
  Models with more parameters generally sustain smaller accuracy drops under the same attack.

## Getting Started

1. Clone the repo and navigate to the project root.  
2. Install dependencies:
   ```bash
   pip install torch torchvision tqdm matplotlib
   ```

