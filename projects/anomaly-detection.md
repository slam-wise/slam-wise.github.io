---
layout: page
title: Industrial Anomaly Detection Case Study
permalink: /projects/anomaly-detection-mvtec/
---

# Industrial Anomaly Detection: Memory-Bank Patch Embeddings for Visual Inspection

In manufacturing environments, anomalous defects (fractures, surface scratches, structural voids) are exceptionally rare. Training standard supervised classification models is impractical due to severe class imbalance.

This project implements an unsupervised visual inspection framework that learns the statistical distribution of normal structural patterns, identifying defects as structural deviations.

---

## 🛠️ Architecture & Feature Extraction

Instead of training an end-to-end network from scratch, the system uses a frozen, pre-trained convolutional backbone to extract deep multi-scale patch features:

1. **Multi-Scale Extraction:** Middle-layer feature maps are extracted to capture both high-resolution local texture details and broader global structural topology.
2. **Patch Embedding Blocks:** Feature maps are processed into uniform patch embedding vectors, capturing localized spatial characteristics across the entire image grid.
3. **Core Memory Bank:** To reduce memory overhead during inference, a patch reduction algorithm sub-samples the nominal embeddings down to a compact, representative memory bank of optimal normal features.

---

## 🔍 Anomaly Detection & Segmentation

During inference, a test image passes through the exact same feature extraction pipeline:

* **Distance Scoring:** The patch embeddings of the test image are compared mathematically against the nominal memory bank using a nearest-neighbor distance calculation.
* **Localization Map:** The computed distance scores are projected back onto the spatial layout of the image to generate a high-resolution anomaly heatmap, pinpointing the precise pixel location of defects.

---

*[View the complete pipeline implementation and test scripts on GitHub.](https://github.com/slam-wise/anomaly-detection-mvtec)*