# Advanced Driver Assistance System (ADAS) — Tiny Object Detection & Lane Detection  
**Track A Submission | Tiny Detector + Lane Detection Baseline**  
**Author:** Shashank  

---

##  Project Overview  
This repository showcases the implementation of a **lightweight perception pipeline** for Advanced Driver Assistance Systems (ADAS).  
It integrates two key components:
1. **Tiny Object Detection** — Detecting *cars* and *persons* using a YOLOv8n-based lightweight model.  
2. **Lane Detection Baseline** — Implementing a simple yet effective *Canny + Hough Transform* approach for lane line extraction.  

The project emphasizes **computational efficiency, real-time inference**, and **robustness under constrained edge hardware environments**.

---

##  Architecture Overview  

**Pipeline Components:**  
1. **Data Preparation:** Small open-source dataset (Roboflow variant with “car” and “person” classes).  
2. **Model Training:** YOLOv8n (Nano) architecture trained for 30 epochs.  
3. **Model Export:** Exported to both `.onnx` and quantized `.onnx (INT8)` formats.  
4. **Evaluation:** Measured **mAP@0.5**, **FPS on CPU**, **model size**, and **false positives**.  
5. **Bonus:** Canny + Hough lane detection evaluated on ~20 top-view road frames.  

---

## Dataset Details

This project uses a **Roboflow Universe dataset** containing images of cars and persons.  

- **Dataset Link:** [Car-Person Dataset on Roboflow Universe](https://universe.roboflow.com/duy-tan/car-person-tviqw/dataset/6)  
- **Total Images:** 515  
  - **Training Images:** 354  
  - **Validation Images:** 99  
  - **Test Images:** 62
    
---


## YOLOv8 Training Details

| Parameter            | Value |
|----------------------|-------|
| **Epochs**           | 30 |
| **Image Size**       | 640 × 640 |
| **Batch Size**       | 8 |
| **Optimizer**        | Adam |
| **Learning Rate**    | 0.001 (initial), 0.01 (final) |
| **Data Augmentation**| Enabled |

---

##  Model Information  

| Model Type | File Name | Size (MB) | Description |
|-------------|------------|-----------|--------------|
| YOLOv8n (FP32) | `model_30epochs.pt` | 5.98 MB | Baseline trained model |
| YOLOv8n (ONNX) | `model_30epochs.onnx` | 11.79 MB | Exported for inference |
| YOLOv8n (INT8 Quantized) | `model_int8.onnx` | 3.29 MB | Post-training quantized model |

---

##  Performance Metrics  

| Metric | Value | Description |
|---------|--------|-------------|
| **mAP@0.5** | 0.8964 | Mean Average Precision at IoU=0.5 |
| **Precision** | 0.8843 | Ratio of true positives over all detections |
| **Recall** | 0.7986 | Detection completeness |
| **F1-Score** | 0.839 | Harmonic mean of Precision and Recall |
| **FPS (CPU) for YOLO** | 58.50 | Frames processed per second on CPU |
| **FPS (CPU) for ONNX** | 7.57 | Frames processed per second on CPU |
| **False Positives During Testing** | 48 detections | Evaluated on unseen validation set |

> These metrics were computed using the YOLO evaluation framework and validated against the ground-truth annotations in the test split.

---


## Validation Metrics

## Validation Metrics and Plots

| Metric / Curve             | Description                         | Figure |
|----------------------------|-------------------------------------|--------|
| **Precision (P)**          | Model precision across thresholds    | ![Precision Curve](metrics/BoxP_curve.png) |
| **Recall (R)**             | Model recall across thresholds       | ![Recall Curve](metrics/BoxR_curve.png) |
| **Precision-Recall (PR)**  | Combined precision-recall behavior   | ![PR Curve](metrics/BoxPR_curve.png) |
| **F1 Score**               | F1 score across thresholds           | ![F1 Curve](metrics/BoxF1_curve.png) |
| **Confusion Matrix**       | True vs predicted class comparison   | ![Confusion Matrix](metrics/confusion_matrix.png) |


---

##  Results  

### YOLO Object Detection
The YOLOv8n model outputs bounding boxes for cars and persons on the test images. Sample results are available in the `results` folder.  

 **Full YOLO Detection Results:** [Drive Folder Link](https://drive.google.com/drive/folders/1gzNjQhYQSOPThAdIPq23AtxeERqVYA7M?usp=sharing)

### Lane Detection
Lane detection results were generated using the Canny + Hough transform pipeline. Sample outputs are stored in the `results/` folder as images with detected lane lines.  

 **Full Lane Detection Results:** [Drive Folder Link](https://drive.google.com/drive/folders/1PZhlPxTXV_OMU1IUESQkh3PdSKOLOMu-?usp=sharing)




