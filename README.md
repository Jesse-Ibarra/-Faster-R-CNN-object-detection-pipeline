# -Faster-R-CNN-object-detection-pipeline
# Faster R-CNN Hyperparameter Optimization & Transfer Learning

## Overview
This project implements and optimizes a Faster R-CNN object detection model using PyTorch. The goal was to improve detection performance on the COCO MiniTrain dataset and evaluate how well the model generalizes to a different domain (drone imagery).

The project focuses on applying practical machine learning techniques including hyperparameter optimization, experiment tracking, and transfer learning.

---

## Key Features
- Faster R-CNN implementation using PyTorch
- Hyperparameter optimization with Optuna (TPE + pruning)
- Experiment tracking using Weights & Biases (W&B)
- Evaluation using COCO metrics (mAP, AP50, AP75, recall)
- Transfer learning evaluation on drone dataset (small object detection)

---

## Tech Stack
- Python
- PyTorch
- Optuna
- Weights & Biases (W&B)
- COCO API (pycocotools)

---

## Dataset
- **Primary Dataset:** COCO MiniTrain (subset of COCO dataset)
- **Transfer Dataset:** Drone imagery dataset (COCO format)

Data preprocessing included:
- Filtering annotations for subset
- Creating deterministic train/validation splits
- Applying standard transformations for object detection

---

## Methodology

### 1. Baseline Model
- Implemented Faster R-CNN with default parameters
- Evaluated performance on validation set using COCO metrics

### 2. Hyperparameter Optimization
Used Optuna with:
- TPE sampler
- Pruning for early stopping

Optimized parameters included:
- Learning rate
- Weight decay
- Momentum
- Gradient clipping
- RPN thresholds and sampling parameters
- ROI head parameters
- Loss weights and post-processing thresholds

### 3. Experiment Tracking
- Logged all runs using W&B
- Compared multiple trials and configurations
- Selected best configuration based on validation mAP

### 4. Final Training
- Retrained best configuration using multiple seeds
- Reported mean and standard deviation of performance

### 5. Transfer Learning (Drone Dataset)
- Evaluated trained model on drone dataset without retuning
- Measured:
  - mAP
  - AP50
  - Recall

---

## Results

### COCO MiniTrain Performance
- mAP: ~0.10
- AP50: ~0.15
- AP75: ~0.11

### Observations
- Hyperparameter tuning provided measurable improvements over baseline
- Performance varied across initialization seeds, highlighting model sensitivity

### Drone Dataset Performance
- Lower detection accuracy due to domain shift
- Common issues observed:
  - Missed small objects
  - Low-confidence detections
  - Duplicate detections (NMS limitations)

---

## Key Learnings
- Hyperparameter tuning significantly impacts object detection performance
- Small object detection remains a challenging problem
- Models trained on general datasets struggle with domain-specific data
- Experiment tracking is essential for comparing model performance
- Initialization randomness can lead to noticeable performance variance

---

## Future Improvements
- Fine-tune model specifically on drone dataset
- Improve small object detection using:
  - Feature pyramid adjustments
  - Higher resolution inputs
- Optimize NMS thresholds for better duplicate suppression
- Explore alternative architectures (e.g., RetinaNet, YOLO variants)

---

## How to Run

1. Install dependencies:
```bash
pip install torch torchvision optuna wandb pycocotools


Link to W&B project: https://wandb.ai/jli43-new-jersey-institute-of-technology/faster-rcnn-optuna-coco-minitrain?nw=nwuserjli43
