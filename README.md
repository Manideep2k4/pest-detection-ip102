# pest-detection-ip102
<img width="1785" height="1477" alt="sample_pests" src="https://github.com/user-attachments/assets/30927686-4db8-42d5-b6ec-b27ffa9970e8" />

# 🌾 Agricultural Pest Detection using YOLOv8
### Real-Time Pest Identification for Precision Agriculture in Indian Crop Fields

[![Python](https://img.shields.io/badge/Python-3.12-blue)](https://python.org)
[![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-orange)](https://ultralytics.com)
[![Dataset](https://img.shields.io/badge/Dataset-IP102-green)](https://github.com/xpwu95/IP102)
[![Demo](https://img.shields.io/badge/Demo-HuggingFace-yellow)](https://huggingface.co/Manideep2k4)
[![License](https://img.shields.io/badge/License-MIT-red)](LICENSE)

---

## 📌 Overview

This project presents a fine-tuned **YOLOv8s** model for real-time agricultural pest detection trained on the **IP102 benchmark dataset** — one of the largest and most diverse insect pest datasets available, covering **102 pest classes across 75,222 field images**.

The system is designed for practical deployment in Indian agricultural settings, directly addressing the challenge of reducing pesticide overuse by enabling **precise, image-based pest identification** at the field level.

> **Relevance:** India loses an estimated 15–25% of crop yield annually to pest damage. Early and accurate pest identification enables targeted pesticide application, reducing chemical use by up to 90% — aligned with the YC Summer 2026 problem statement on AI for Low-Pesticide Agriculture.

---

## 📊 Dataset — IP102

| Split | Images | Classes |
|-------|--------|---------|
| Train | 45,095 | 102 |
| Val   | 7,508  | 102 |
| Test  | 22,619 | 102 |
| **Total** | **75,222** | **102** |

The dataset covers major pest species relevant to Indian agriculture including:
- Rice pests: Rice Leaf Roller, Asiatic Rice Borer, Brown Plant Hopper, Yellow Rice Borer
- Wheat pests: Wheat Blossom Midge, Wheat Phloeothrips
- Corn pests: Corn Borer, Corn Earworm
- And 94 more classes across multiple crop types

---

## 🏗️ Methodology

### Model Architecture
- **Base Model:** YOLOv8s (Small) pretrained on COCO
- **Fine-tuning:** Transfer learning on IP102 classification-to-detection pipeline
- **Input Resolution:** 224×224
- **Parameters:** 11.17M

### Training Configuration
```
Optimizer:     AdamW (lr=0.001, weight_decay=0.0005)
Epochs:        50
Batch Size:    64
Image Size:    224×224
Augmentation:  RandomAugment, HSV, Mosaic, Flip
Early Stop:    Patience=10
Hardware:      Tesla T4 GPU (Google Colab)
```

### Dataset Preparation
IP102 is originally a classification dataset. We converted it to YOLO detection format using full-image bounding boxes (cx=0.5, cy=0.5, w=1.0, h=1.0) per class label — a standard approach for classification-to-detection transfer when per-object bounding box annotations are unavailable.

---

## 📈 Results

| Metric | Value |
|--------|-------|
| mAP@50 | **61.6%** |
| mAP@50-95 | **61.4%** |
| Precision | **63.7%** |
| Recall | **56.5%** |
| Inference Speed | ~15ms/image (T4 GPU) |

### Training Curve
| Epoch | mAP@50 |
|-------|--------|
| 1     | 0.087  |
| 10    | 0.400  |
| 20    | 0.527  |
| 26    | 0.557  |
| 50    | **0.616** ✅ |

---

## 🚀 Quick Start

### Installation
```bash
git clone https://github.com/Manideep2k4/pest-detection-ip102
cd pest-detection-ip102
pip install ultralytics gradio
```

### Run Inference
```python
from ultralytics import YOLO

model = YOLO('weights/best.pt')
results = model.predict('your_pest_image.jpg', conf=0.5)
results[0].show()
```

### Run Demo Locally
```bash
python app.py
```

---

## 🌐 Live Demo

👉 **[Try the live demo on Hugging Face Spaces](https://huggingface.co/spaces/Manideep2k4/pest-detection)**

Upload any crop field image and get real-time pest identification with confidence scores.

---

## 📁 Repository Structure

```
pest-detection-ip102/
├── train.py              # Training script
├── evaluate.py           # Evaluation on test set
├── app.py                # Gradio demo
├── ip102.yaml            # Dataset configuration
├── weights/
│   └── best.pt           # Best model weights
├── results/
│   ├── confusion_matrix.png
│   ├── training_curves.png
│   └── sample_predictions/
└── README.md
```

---

## 🔗 Related Work

This project is an extension of published research in agricultural AI:

> **Parvatini Manideep et al.**, *"A Domain-Adapted Multi-Source Ensemble Framework for Real-Time Crop Recommendation in Indian Agro-Zones"*, ICISESSC-2026.

> **Parvatini Manideep**, *"Machine Learning for Agentic Behavior"*, Book Chapter in *Autonomous Intelligence: Designing the Future of Agentic Systems* (In Press, copyright signed).

---

## 🌱 Applications

- **Precision Farming:** Identify pests before significant crop damage occurs
- **Pesticide Reduction:** Target spraying only where pests are detected
- **Mobile Deployment:** Lightweight YOLOv8s suitable for edge devices used by farmers
- **Government Integration:** Compatible with ICAR and digital agriculture initiatives

---

## 🔮 Future Work

- [ ] District-level model fine-tuning for Indian agro-zones
- [ ] Integration with satellite/drone imagery (NDVI + pest detection fusion)
- [ ] Edge deployment via TensorFlow Lite for low-connectivity rural areas
- [ ] Fertilizer recommendation integration (extending crop paper pipeline)
- [ ] Real-time mobile app for farmers

---

## 👤 Author

**Parvatini Manideep**
B.Tech CSE, Lovely Professional University
📧 manideep2k4@gmail.com
🔗 [LinkedIn](https://linkedin.com/in/manideepp/) | [GitHub](https://github.com/Manideep2k4)

---

## 📄 License

MIT License — free to use for research and educational purposes.

---

*If you find this useful, please ⭐ the repository.*
