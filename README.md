# GAN Training Stability and Image-to-Image Translation

## Project Overview
The objective of this project is to study **training stability in Generative Adversarial Networks (GANs)** and implement **image-to-image translation** using modern deep learning architectures. The project compares baseline GAN methods with advanced techniques to mitigate instability issues such as **mode collapse**, while also implementing both **paired** and **unpaired** image translation models.

---

# 1. Tackling Mode Collapse (DCGAN vs WGAN-GP)

## Objective
Design and implement GAN architectures that address **mode collapse** and improve training stability.

Mode collapse occurs when the generator produces limited variations of images, reducing diversity in generated outputs. The goal is to compare a standard GAN with an improved architecture that stabilizes the training process.

## Models

### Baseline Model: DCGAN
Deep Convolutional GAN (DCGAN) uses convolutional layers for stable image generation.

**Key Characteristics**
- Loss Function: Binary Cross Entropy (BCE)
- Generator: Transposed convolutions for upsampling
- Discriminator: Convolutional classifier
- Activation:
  - Generator: ReLU
  - Output Layer: Tanh
  - Discriminator: LeakyReLU

### Advanced Model: WGAN-GP
Wasserstein GAN with Gradient Penalty improves convergence stability and reduces mode collapse.

**Key Characteristics**
- Uses a **Critic** instead of a discriminator
- Loss Function: Wasserstein Loss
- Gradient Penalty enforces Lipschitz constraint
- Provides smoother and more stable training dynamics

## Dataset Options
- Pokemon Sprites (64×64)
- Anime Faces (64×64)

---

# 2. Paired Image Translation (Pix2Pix)

## Objective
Implement a **conditional GAN** that learns a mapping between paired image domains such as:

- Sketch → Colored Image
- Grayscale → RGB Image

Pix2Pix uses supervised learning with aligned input-output image pairs.

## Architecture

### Generator: U-Net
- Encoder-decoder structure
- Skip connections preserve spatial details
- Helps retain texture and structure from input image

### Discriminator: PatchGAN
- Classifies local patches instead of full images
- Focuses on high-frequency realism
- Encourages sharper outputs

## Dataset Options
- CUHK Face Sketch Dataset
- Anime Sketch Colorization Dataset

---

# 3. Unpaired Image Translation (CycleGAN)

## Objective
Learn mappings between two image domains **without paired data**.

Example tasks:
- Sketch ↔ Photo
- Painting ↔ Real Image
- Day ↔ Night

CycleGAN learns transformations using cyclic reconstruction constraints.

## Architecture

### Generators
- ResNet-based architecture
- 6 residual blocks
- Two generators:
  - G: Domain X → Domain Y
  - F: Domain Y → Domain X

### Loss Functions

1. Adversarial Loss
   - Ensures generated images resemble target domain

2. Cycle Consistency Loss
   - Ensures transformation preserves content

3. Identity Loss
   - Preserves color composition and structure

## Dataset Options
- TU-Berlin Sketch Dataset
- Sketchy Dataset
- Google QuickDraw Dataset

---

# Implementation Details

## Environment Setup

Platform:
- Kaggle Notebook

Hardware:
- Dual GPU T4 ×2

Mixed Precision Training:
- torch.cuda.amp
- Reduces memory usage
- Speeds up training

---

## Training Strategy

Optimizer:
- Adam Optimizer

Hyperparameters:
- Learning Rate: 0.0002
- Betas: (0.5, 0.999)

Image Sizes:
- GANs: 64×64
- Pix2Pix: 256×256
- CycleGAN: 128×128

Checkpointing:
- Models saved every 5–10 epochs

---

# Evaluation Metrics

Quantitative Metrics for Image Translation:

## SSIM (Structural Similarity Index)
Measures similarity between generated image and ground truth.

Range:
0 → No similarity  
1 → Perfect similarity

## PSNR (Peak Signal-to-Noise Ratio)
Measures reconstruction quality.

Higher PSNR indicates better quality.

---

# Deliverables

## 1. Jupyter Notebooks
Complete PyTorch implementations for:

- DCGAN
- WGAN-GP
- Pix2Pix
- CycleGAN

Each notebook includes:
- Model architecture
- Training loop
- Loss calculations
- Visualization of generated outputs

---

## 2. Training Logs

Plots showing:

- Generator Loss vs Epochs
- Discriminator/Critic Loss vs Epochs
- Training stability comparisons

---

## 3. Evaluation Results

Quantitative analysis including:

- SSIM scores
- PSNR scores
- Visual comparisons of generated outputs

---

## 4. Deployment Application

Interactive demo using:

- Gradio OR Streamlit

Features:
- Upload input image
- Real-time generated output
- Adjustable parameters (optional)

---

# Expected Learning Outcomes

By completing this project, you will:

- Understand GAN instability problems
- Compare BCE vs Wasserstein loss
- Implement conditional GANs
- Learn domain adaptation without paired data
- Evaluate image quality using SSIM and PSNR
- Deploy deep learning models using Gradio or Streamlit

---

# Tech Stack

Programming Language:
- Python

Libraries:
- PyTorch
- torchvision
- numpy
- matplotlib
- scikit-image
- gradio or streamlit

Compute Platform:
- Kaggle GPU Environment
