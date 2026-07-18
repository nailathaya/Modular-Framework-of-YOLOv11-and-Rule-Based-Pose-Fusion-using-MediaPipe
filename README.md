# Enhancing Armed Person Detection Using YOLOv11 and Rule-Based Pose Fusion in a Modular Framework

Implementation of my undergraduate thesis on improving armed person detection by combining **YOLOv11** object detection with **MediaPipe Pose Estimation** using a **rule-based fusion** strategy in a modular architecture.

This repository contains the complete training, evaluation, and fusion pipeline for detecting armed persons using a custom weapon dataset.

---

## Overview

Detecting armed persons in surveillance images is challenging because firearms are often:

- Small objects
- Partially occluded
- Located close to the human body
- Difficult to distinguish from surrounding objects

To address these challenges, this project combines object detection and human pose estimation in a modular framework.

The proposed system consists of two independent modules:

1. **YOLOv11** for object detection
2. **MediaPipe Pose** for extracting body keypoints

The outputs from both modules are integrated using a lightweight **rule-based pose fusion** algorithm to improve detection robustness.

---

## Methodology

The proposed pipeline consists of:

```
Input Image
      │
      ▼
YOLOv11 Detection
      │
      ├── Person Holding Weapon
      └── Weapon
      │
      ▼
MediaPipe Pose Estimation
      │
      ▼
Body Keypoint Extraction
(Wrist & Elbow)
      │
      ▼
Rule-Based Pose Fusion
      │
      ▼
Final Detection
```

The fusion module performs:

- Weapon validation using wrist proximity
- Missed weapon recovery using elbow-to-wrist direction
- Confidence adjustment based on spatial relationship
- Modular integration without retraining the detector

---

## Features

- YOLOv11 object detector
- MediaPipe Pose Landmarker
- Rule-based pose fusion
- Modular architecture
- Automatic evaluation
- Precision-Recall Curve generation
- Visualization of:
  - Weapon bounding boxes
  - Human pose keypoints
  - Arm skeleton

---

## Dataset

The project uses a custom armed-person dataset containing two classes:

| Class | ID |
|--------|----|
| person hold weapon | 0 |
| weapon | 1 |

Dataset structure:

```
dataset/
    train/
        images/
        labels/
    valid/
        images/
        labels/
    test/
        images/
        labels/
```

---

## Installation

```bash
pip install ultralytics
pip install mediapipe
pip install opencv-python
pip install matplotlib
pip install tqdm
```

---

## Training

Train YOLOv11:

```python
model.train(...)
```

After training, the best model is stored in:

```
weights/best.pt
```

---

## Fusion Pipeline

The fusion module performs the following steps:

1. Detect weapons using YOLOv11
2. Extract wrist and elbow keypoints using MediaPipe
3. Validate detected weapons based on wrist proximity
4. Recover missed detections using arm direction estimation
5. Produce the final detection results

---

## Output Visualization

The pipeline automatically saves visualization results including:

- Weapon bounding boxes
- Confidence scores
- Pose keypoints
- Arm skeleton

---

## Evaluation Metrics

The system is evaluated using:

- Precision
- Recall
- mAP@50
- Precision-Recall Curve

---

## Example Results

### Baseline YOLOv11

| Metric | Score |
|---------|------:|
| Precision | 0.913 |
| Recall | 0.707 |
| mAP50 | 0.751 |

### Proposed Fusion

| Metric | Score |
|---------|------:|
| Precision | 0.760 |
| Recall | **0.801** |
| mAP50 | **0.751** |

The proposed fusion significantly improves recall while maintaining comparable mAP, demonstrating better sensitivity in detecting previously missed weapon instances.

---

## Thesis

**Title**

> *Peningkatan Deteksi Orang Bersenjata Menggunakan YOLOv11 dan Fusi Pose Berbasis Aturan dalam Kerangka Modular*

English title:

> *Enhancing Armed Person Detection Using YOLOv11 and Rule-Based Pose Fusion in a Modular Framework*

---

## Author

**Naila Athaya Mumtaz**

School of Computing

Telkom University

Bandung, Indonesia

## Co-Author
**Bedy Purnama** <sup>1,</sup><sup>2</sup>

<sup>1</sup>School of Computing

Telkom University

Bandung, Indonesia

<sup>2</sup>Center of Excellence of Artificial Intelligence for Learning and Optimization

Telkom University

Bandung, Indonesia


---

## License

This project is intended for academic and research purposes.
