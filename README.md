# C2ICARE‑Optimized YOLO for Real‑Time Marine Species Detection via Multi‑Scale Convolutional Design

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Ultralytics](https://img.shields.io/badge/Ultralytics-YOLO26n-00BFFF.svg)](https://github.com/ultralytics/ultralytics)

**Official implementation of C2ICARE (Convolution to Interactive Capture and Re‑calibration Enhancement), a multi‑scale convolutional module that optimizes YOLO for real‑time marine species detection. It surpasses the YOLO26n baseline in accuracy by 12% while reducing GFLOPs by 1.9%.**

---

## 📢 Updates

- `[Date]`: 🚀 Initial release of code and pretrained weights
- `[Date]`: 📄 Paper accepted at [Conference/Journal Name]

---

## 🏗️ Architecture

### Complete Model Architecture

**Figure 1** shows the detailed architecture of the proposed YOLO26n-based model, integrating FasterBlock, C2ICARE, and C3Ghost modules for optimized fish detection in underwater cameras.

<p align="center">
  <img src="figures/architecture_complete.png" alt="Complete YOLO26n architecture with FasterBlock, C2ICARE, and C3Ghost modules" width="800">
  <br>
  <em>Figure 1. Detailed architecture of the proposed YOLO26n-based model, integrating FasterBlock, C2ICARE, and C3Ghost modules for optimized fish detection in underwater cameras.</em>
</p>

### C2ICARE Module

<!-- Aquí pondrás la segunda figura solo del módulo C2ICARE -->

<p align="center">
  <img src="figures/c2icare_module.png" alt="C2ICARE module internal architecture" width="600">
  <br>
  <em>Figure 2. Internal architecture of the proposed C2ICARE module.</em>
</p>

---

## 📊 Experimental Results

### Data Augmentation

To simulate the variability of underwater lighting conditions, HSV shifts were applied with a hue shift range of ±0.5 and a saturation multiplier ranging from 0 to 2.

<p align="center">
  <img src="figures/hsv_augmentation.png" alt="HSV augmentation grid" width="600">
  <br>
  <em>Figure 3. HSV augmentation grid for hue shift versus saturation factor.</em>
</p>

### Training Performance

**Figure 4** shows the mAP@0.5 progression over 50 epochs for all model variants (M0–M9), averaged across three independent runs (random seeds 0, 1, and 2).

<p align="center">
  <img src="figures/mAP50_progress.png" alt="mAP@0.5 progression over 50 epochs" width="700">
  <br>
  <em>Figure 4. Mean Average Precision (mAP@0.5) performance progress over 50 epochs, averaged across three independent runs (random seeds 0, 1, and 2). M0 represents the YOLOv8n baseline; M1 denotes the YOLO11n baseline; M2 is the YOLO26n baseline; M3 is YOLO26n + FasterBlock; M4 is YOLO26n + C2ICARE; M5 is YOLO26n + C3Ghost; M6 is YOLO26n + FasterBlock + C2ICARE; M7 is YOLO26n + C2ICARE + C3Ghost; M8 is YOLO26n + FasterBlock + C3Ghost; and M9 is YOLO26n + FasterBlock + C2ICARE + C3Ghost.</em>
</p>

### Performance Metrics

**Table 2** summarizes the performance metrics and computational complexity for all model configurations on the test split.

| Model | FasterBlock | C2ICARE | C3Ghost | mAP@0.5 | mAP@0.5:0.95 | Precision | Recall | Parameters | GFLOPs |
|-------|-------------|---------|---------|---------|--------------|-----------|--------|------------|--------|
| M0 | | | | 0.5571 | 0.3071 | 0.5374 | 0.5853 | 3,006,428 | 8.088 |
| M1 | | | | 0.4892 | 0.2474 | 0.4795 | 0.5263 | 2,582,932 | 6.316 |
| M2 | | | | 0.5777 | 0.3325 | 0.5740 | 0.5475 | 2,375,616 | 5.193 |
| M3 | ✓ | | | 0.5672 | 0.3214 | 0.5617 | 0.5442 | 2,319,296 | 5.125 |
| M4 | | ✓ | | 0.6369 | 0.3715 | 0.6217 | 0.6034 | 2,334,112 | 5.160 |
| M5 | | | ✓ | 0.5798 | 0.3376 | 0.5658 | 0.5477 | 2,089,248 | 4.964 |
| M6 | ✓ | ✓ | | 0.6375 | 0.3800 | 0.6248 | 0.6029 | 2,277,792 | 5.093 |
| M7 | | ✓ | ✓ | 0.5550 | 0.3125 | 0.5356 | 0.5274 | 2,047,744 | 4.931 |
| M8 | ✓ | | ✓ | 0.5541 | 0.3137 | 0.5268 | 0.5740 | 2,032,928 | 4.897 |
| M9 | ✓ | ✓ | ✓ | 0.5406 | 0.3079 | 0.5230 | 0.5458 | 1,991,424 | 4.864 |

*M0 represents the YOLOv8n baseline; M1 denotes the YOLO11n baseline; M2 is the YOLO26n baseline. M3 to M9 are the proposed YOLO26n architectural variants.*

### Multi‑Objective Performance

**Figure 6** presents a radial performance comparison of all YOLO architectures (M0–M9). The GFLOPs axis is inverted such that peripheral placement reflects lower computational demand and enhanced efficiency.

<p align="center">
  <img src="figures/radar_chart.png" alt="Radar chart of multi-objective performance" width="600">
  <br>
  <em>Figure 6. Radial performance comparison of YOLO architectures (M0–M9). The GFLOPs axis is inverted such that peripheral placement reflects lower computational demand and enhanced efficiency.</em>
</p>

### XAI Analysis: EigenCAM Visualisation

**Figure 7** shows EigenCAM visualisations for the proposed M6 model on four test images from the underwater camera dataset. The colour coding for bounding boxes is as follows: mackerel (red), herring (green), bluewhiting (white), mesopelagic (yellow).

<p align="center">
  <img src="figures/eigencam_results.png" alt="EigenCAM visualisation results" width="800">
  <br>
  <em>Figure 7. EigenCAM visualisation for the proposed M6 model (based on YOLO26n) on four test images from the underwater camera dataset. Subfigure (a) shows the original image ST1_135-20180503160446316, and (b) displays its EigenCAM heatmap with coloured bounding boxes, where the model detected 3 bluewhiting, 2 herring, and 1 mesopelagic individual. Subfigure (c) shows the original image ST6_6-20180506204859914, and (d) displays its heatmap with 6 mackerel and 5 herring detections. Subfigure (e) shows the original image ST019-13-20170511204755726, and (f) displays its heatmap with 8 mackerel detection. Subfigure (g) shows the original image ST033-864-607-20170520203304451, and (h) displays its heatmap with 2 bluewhiting and 12 herring detections.</em>
</p>

---

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- CUDA 11.8 (for GPU training)
- PyTorch 1.10+
- Ultralytics YOLOv8.0.117+

### Installation

```bash
git clone https://github.com/VinieLee/C2ICARE-Optimized-YOLO-for-Real-Time-Marine-Species-Detection-via-Multi-Scale-Convolutional-Design.git
cd C2ICARE-Optimized-YOLO-for-Real-Time-Marine-Species-Detection-via-Multi-Scale-Convolutional-Design
pip install -r requirements.txt
