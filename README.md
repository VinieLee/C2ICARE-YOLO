# C2ICARE‑Optimized YOLO for Real‑Time Marine Species Detection via Multi‑Scale Convolutional Design

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Ultralytics](https://img.shields.io/badge/Ultralytics-YOLO26n-00BFFF.svg)](https://github.com/ultralytics/ultralytics)

**Official implementation of C2ICARE (Convolution to Interactive Capture and Re‑calibration Enhancement), a multi‑scale convolutional module that optimizes YOLO for real‑time marine species detection. It surpasses the YOLO26n baseline in accuracy by 12% while reducing GFLOPs by 1.9%.**

---

## 📢 Updates

- `April 2026`: 🚀 Initial release of code and pretrained weights
- `April 2026`: 📄 Paper available

---

## 🏗️ Architecture

### Complete Model Architecture

**Figure 1** shows the detailed architecture of the proposed YOLO26n-based model, integrating FasterBlock, C2ICARE, and C3Ghost modules.

<p align="center">
  <img src="figures/YOLO26+FasterBlock+C2ICARE.png" alt="Complete YOLO26n architecture" width="800">
  <br>
  <em>Figure 1. Detailed architecture of the proposed YOLO26n-based model.</em>
</p>

### C2ICARE Module

<p align="center">
  <img src="figures/C2ICARE_module.png" alt="C2ICARE module internal architecture" width="100">
  <br>
  <em>Figure 2. Internal architecture of the proposed C2ICARE module.</em>
</p>

---

## 📊 Experimental Results

### Data Augmentation

<p align="center">
  <img src="figures/HSV_5x5_Hue_vs_Saturation.png" alt="HSV augmentation grid" width="600">
  <br>
  <em>Figure 3. HSV augmentation grid for hue shift versus saturation factor.</em>
</p>

### Training Performance

<p align="center">
  <img src="figures/mAP50_VS_Epoch.png" alt="mAP@0.5 progression over 50 epochs" width="700">
  <br>
  <em>Figure 4. Mean Average Precision (mAP@0.5) performance progress over 50 epochs, averaged across three independent runs (random seeds 0, 1, and 2).</em>
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

<p align="center">
  <img src="figures/Radar_Plot.png" alt="Radar chart of multi-objective performance" width="600">
  <br>
  <em>Figure 6. Radial performance comparison of YOLO architectures (M0–M9). The GFLOPs axis is inverted such that peripheral placement reflects lower computational demand and enhanced efficiency.</em>
</p>

### XAI Analysis: EigenCAM Visualisation

**Figure 7** shows EigenCAM visualisations for the proposed M6 model on test images from the underwater camera dataset. The colour coding for bounding boxes is as follows: mackerel (red), herring (green), bluewhiting (white), mesopelagic (yellow).

<p align="center">
  <img src="figures/EigenCAM_3columns_ST1_135-20180503160446316.jpg" alt="EigenCAM ST1_135" width="800">
  <br>
  <em>Figure 7a. EigenCAM visualisation for ST1_135-20180503160446316: 3 bluewhiting, 2 herring, 1 mesopelagic.</em>
</p>

<p align="center">
  <img src="figures/EigenCAM_3columns_ST6_6-20180506204859914.jpg" alt="EigenCAM ST6_6" width="800">
  <br>
  <em>Figure 7b. EigenCAM visualisation for ST6_6-20180506204859914: 6 mackerel, 5 herring.</em>
</p>

<p align="center">
  <img src="figures/EigenCAM_3columns_ST019-13-20170511204755726.jpg" alt="EigenCAM ST019-13" width="800">
  <br>
  <em>Figure 7c. EigenCAM visualisation for ST019-13-20170511204755726: 8 mackerel.</em>
</p>

<p align="center">
  <img src="figures/EigenCAM_3columns_ST033-864-607-20170520203304451.jpg" alt="EigenCAM ST033-864" width="800">
  <br>
  <em>Figure 7d. EigenCAM visualisation for ST033-864-607-20170520203304451: 2 bluewhiting, 12 herring.</em>
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
```

###Dataset Preparation
```
📁 your_dataset/
├── 📁 images/
│   ├── 📁 train/
│   ├── 📁 val/
│   └── 📁 test/
├── 📁 labels/
│   ├── 📁 train/
│   ├── 📁 val/
│   └── 📁 test/
└── 📄 data.yaml
```
###📄 License

This project is licensed under the GNU Affero General Public License v3.0 - see the LICENSE file for details.
This license requires that if you modify the code and provide a service over a network (e.g., a web API), you must make the complete source code available to users under the same license.

###📚 Citation
```bash
@article{SilvaAlvarado2026C2ICARE,
  title={C2ICARE‑Optimized YOLO for Real‑Time Marine Species Detection via Multi‑Scale Convolutional Design},
  author={Silva-Alvarado, Vinie Lee and Ahmad, Ali and Sendra, Sandra and Lloret, Jaime},
  journal={[Journal Name]},
  year={2026},
  note={Under review}
}
```




