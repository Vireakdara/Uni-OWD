# YOLO-UniOW: Efficient Universal Open-World Object Detection

## Overview
**YOLO-UniOW** introduces **Universal Open-World Object Detection (Uni-OWD)**, unifying **open-vocabulary detection (OVD)** and **open-world detection (OWOD)** into a single framework. It addresses the limitations of traditional detectors (fixed vocabularies) and multimodal models (high computational costs) by enabling:
- Detection of **known** and **unknown** objects (labeled as "unknown").
- Dynamic vocabulary expansion without retraining.
- Real-time inference (up to **69.6 FPS** on V100 GPUs).
![image](https://github.com/user-attachments/assets/88e68af7-2140-402f-988d-e2f2fa300799)

---

## Key Features

### 1. **Adaptive Decision Learning (AdaDL)**
- **Lightweight CLIP Alignment**: Replaces cross-modality fusion (e.g., RepVL-PAN) with alignment in the CLIP latent space.
- **Parameter Efficiency**: Uses **LoRA (Low-Rank Adaptation)** to fine-tune the CLIP text encoder, preserving generalization while adapting decision boundaries.
- **Dual-Head Matching**: Aligns region proposals from YOLOv10’s one-to-one and one-to-many heads with text embeddings.

### 2. **Wildcard Learning**
- **Unknown Detection**: Trains a "wildcard" embedding (`T_unk`) to detect out-of-distribution objects via self-supervised pseudo-labeling.
- **Dynamic Expansion**: Converts high-confidence "unknown" predictions into new known classes iteratively.
- **Filtering Strategy**: Removes duplicate predictions using IoU thresholds and similarity scores.

### 3. **Efficiency Enhancements**
- **YOLOv10 Backbone**: Leverages NMS-free training and consistent dual assignments for faster inference.
- **No Fusion Overhead**: Eliminates RepVL-PAN, reducing parameters (e.g., **29.4M** for YOLO-UniOW-L vs. **48M** for YOLO-World-L).

---
