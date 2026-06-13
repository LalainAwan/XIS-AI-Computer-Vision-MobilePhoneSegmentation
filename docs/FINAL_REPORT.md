# Mobile Phone Segmentation and Dimension Measurement Using Mask R-CNN

## XIS AI Computer Vision Assessment

---

# 1. Introduction

Computer vision enables machines to understand and interpret visual information from images and videos. One important application is object segmentation, where individual objects are identified and separated from the background at the pixel level.

This project implements a complete computer vision pipeline for mobile phone segmentation and dimension estimation using camera calibration and deep learning. The workflow includes camera calibration, dataset collection, image annotation, instance segmentation using Mask R-CNN, model evaluation, and real-world dimension measurement.

The objective is to accurately segment a mobile phone from images and estimate its physical dimensions using calibrated imagery.

---
#Figure 1: End-to-End Measurement Pipeline
## Figure 1. End-to-End Measurement Pipeline

![Pipeline Architecture](images/pipeline_architecture.png)

# 2. Object Selection

The selected object for this project is an iPhone 12 Mini.

The phone was chosen because:

* It has a well-defined rectangular shape.
* It is easy to photograph from multiple viewpoints.
* Its dimensions can be measured accurately for validation.

## Ground Truth Measurements

Physical measurements were obtained using a ruler.

| Dimension | Measurement |
| --------- | ----------- |
| Height    | 131 mm      |
| Width     | 64 mm       |
| Thickness | 7 mm        |

---

# 3. Camera Calibration

Camera calibration was performed to estimate the intrinsic parameters of the camera and correct lens distortion.

## Calibration Pattern

A checkerboard pattern was printed on an A4 sheet and mounted on cardboard.

### Checkerboard Specifications

* Squares Across: 11
* Squares Down: 7
* Square Size: 20 mm

## Calibration Procedure

1. Multiple images of the checkerboard were captured from different angles.
2. Checkerboard corners were detected using OpenCV.
3. Object points and image points were collected.
4. Camera intrinsic parameters were computed.
5. Lens distortion coefficients were estimated.
6. Reprojection error was calculated.

## Calibration Results

### Successful Detections

25 / 25 images

### Camera Matrix

[
\begin{bmatrix}
991.7444 & 0 & 480.6319 \
0 & 990.4081 & 635.1348 \
0 & 0 & 1
\end{bmatrix}
]

### Distortion Coefficients

[
[0.1336,\ -0.7166,\ -0.0016,\ -0.0014,\ 0.5754]
]

### Mean Reprojection Error

0.2377 pixels

## Calibration Analysis

The low reprojection error indicates that the calibration process was successful and that the estimated camera parameters accurately model the imaging system.

---

# 4. Dataset Collection

A custom dataset was created specifically for mobile phone segmentation.

## Device Used

* iPhone 12 Mini

## Image Collection Strategy

Images were captured under varying conditions:

* Multiple orientations
* Different viewing angles
* Different distances
* Different backgrounds
* Indoor lighting conditions

## Dataset Size

| Dataset Split | Images |
| ------------- | ------ |
| Training      | 56     |
| Validation    | 16     |
| Testing       | 8      |
| Total         | 80     |

---

# 5. Dataset Annotation

Image annotation was performed using Roboflow.

## Annotation Type

* Polygon Segmentation

## Export Format

* COCO Segmentation

## Class Labels

Only one object class was used:

* mobile_phone

## Annotation Procedure

Each image was manually annotated using polygon segmentation around the visible boundaries of the phone.

The annotations were exported in COCO segmentation format for compatibility with Mask R-CNN.

---

# 6. Model Development

## Selected Model

Mask R-CNN with ResNet50-FPN Backbone

## Reason for Selection

Mask R-CNN was selected because:

* Provides pixel-level object masks.
* Supports instance segmentation.
* Produces accurate object boundaries.
* Suitable for object measurement tasks.

---

# 7. Model Training

## Training Configuration

| Parameter     | Value             |
| ------------- | ----------------- |
| Optimizer     | Adam              |
| Learning Rate | 0.0001            |
| Batch Size    | 2                 |
| Epochs        | 10                |
| Framework     | PyTorch           |
| Hardware      | NVIDIA GPU (CUDA) |

## Training Results

### Final Training Loss

0.0720

### Final Validation Loss

0.1972

## Model Output

Trained model:

mask_rcnn_mobile_phone.pth

## Training Analysis

The training loss decreased steadily over successive epochs, indicating successful learning.

The validation loss remained low throughout training, suggesting good generalization to unseen data.

---

# 8. Model Evaluation

The trained model was evaluated on the test dataset containing 8 previously unseen images.

## Evaluation Metrics

### Mean Intersection over Union (IoU)

0.9196

### Precision

1.0000

### Recall

1.0000

### F1 Score

1.0000

## Evaluation Analysis

The Mean IoU score of 0.9196 indicates excellent overlap between predicted segmentation masks and the ground truth annotations.

The model achieved perfect Precision and Recall on the test set, resulting in an F1 Score of 1.0000.

These results demonstrate that the model successfully learned the appearance and boundaries of the mobile phone object.

---

# 9. Inference Results

The trained model was tested on unseen images.

## Inference Pipeline

1. Load image.
2. Run Mask R-CNN inference.
3. Generate segmentation mask.
4. Extract bounding box.
5. Estimate object dimensions.

## Detection Confidence

Example prediction confidence:

0.9991

The high confidence score demonstrates strong model certainty when detecting the target object.

---

# 10. Dimension Estimation

The segmentation mask was used to extract object boundaries from the image.

A pixel-to-millimeter conversion approach was then applied using the known dimensions of the phone.

## Ground Truth Dimensions

| Dimension | Value  |
| --------- | ------ |
| Height    | 131 mm |
| Width     | 64 mm  |
| Thickness | 7 mm   |

## Measurement Workflow

1. Segment phone using Mask R-CNN.
2. Generate object mask.
3. Compute bounding box dimensions.
4. Convert pixel measurements to millimeters.
5. Compare against ground truth measurements.

## Discussion

The experiment demonstrates that segmentation masks can be used for object measurement and dimensional analysis.

Accurate calibration and segmentation are critical for obtaining reliable measurements.

---

# 11. Challenges Encountered

Several challenges were encountered during development:

### Camera Calibration

Initial calibration images produced poor corner detections and high reprojection error.

### Dataset Quality

Some images contained motion blur or incomplete object visibility and were removed from the dataset.

### Annotation Consistency

Polygon boundaries required careful adjustment to accurately follow the phone edges.

### Model Training

Dataset loading and annotation path issues required debugging before successful training.

---

# 12. Limitations

The current implementation has several limitations:

* Small dataset size.
* Single object category.
* Controlled indoor environment.
* Pixel-to-millimeter scaling relies on known object dimensions.
* Thickness estimation is limited from single-view imagery.

 Future work should evaluate multiple images and viewing conditions to compute Mean Absolute Error (MAE) and Mean Percentage Error (MPE).

---

# 13. Future Improvements

Potential improvements include:

* Larger dataset.
* Additional object categories.
* Automatic scale estimation.
* Multi-view reconstruction.
* Real-time deployment.
* Mobile application integration.

---

# 14. Conclusion

This project successfully implemented a complete computer vision pipeline for mobile phone segmentation and dimension estimation.

The workflow included camera calibration, dataset collection, annotation, model training, evaluation, and measurement.

Key achievements include:

* Successful camera calibration with a reprojection error of 0.2377 pixels.
* Creation of a custom dataset containing 80 annotated images.
* Training of a Mask R-CNN segmentation model.
* Mean IoU of 0.9196.
* Precision of 1.0000.
* Recall of 1.0000.
* F1 Score of 1.0000.
* Successful object measurement using segmentation outputs.

The results demonstrate the effectiveness of combining camera calibration and deep learning-based instance segmentation for object analysis and measurement tasks.

---

# References

1. OpenCV Documentation
2. PyTorch Documentation
3. Mask R-CNN Research Paper
4. COCO Dataset Format Documentation
5. Roboflow Annotation Platform Documentation

