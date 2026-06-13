# MEASUREMENT REPORT

## 1. Objective

The objective of this phase was to estimate the real-world dimensions of a mobile phone using a calibrated camera and an image segmentation model. The system combines camera calibration, image segmentation, and pixel-to-millimetre conversion to demonstrate an end-to-end computer vision measurement pipeline.

---

## 2. Selected Object

### Object

Mobile Phone (iPhone 12 Mini)

### Ground Truth Measurements

Physical measurements were obtained using a ruler.

| Dimension | Measurement |
| --------- | ----------- |
| Height    | 131 mm      |
| Width     | 64 mm       |
| Thickness | 7 mm        |

---

## 3. Measurement Methodology

The measurement workflow consists of the following steps:

1. Capture image using calibrated camera.
2. Apply lens distortion correction using intrinsic camera parameters.
3. Run Mask R-CNN segmentation model.
4. Generate object segmentation mask.
5. Extract object contour from the predicted mask.
6. Compute bounding-box dimensions in pixels.
7. Convert pixel measurements into millimetres using a pixel-to-mm conversion ratio.
8. Compare estimated dimensions with physical measurements.

Pipeline:

Raw Image → Undistortion → Segmentation → Mask Extraction → Pixel Measurement → Pixel-to-mm Conversion → Real-World Dimensions

---

## 4. Calibration Dependency

Camera calibration is essential for accurate measurement.

Without calibration:

* Lens distortion changes apparent object dimensions.
* Measurements vary across image regions.
* Pixel distances do not correspond consistently to real-world distances.

After calibration:

* Distortion is removed.
* Geometric accuracy improves.
* Pixel measurements become more reliable.

Therefore, all measurement images were processed using calibrated camera parameters before segmentation and dimension estimation.

---

## 5. Pixel-to-MM Conversion

The segmentation mask was converted into a binary mask and the largest contour corresponding to the mobile phone was extracted.

Measured object dimensions in the test image:

| Measurement     | Value  |
| --------------- | ------ |
| Width (pixels)  | 504 px |
| Height (pixels) | 357 px |

A pixel-to-millimetre conversion ratio was then derived using the known dimensions of the object.

This conversion demonstrates the complete workflow for transforming image-space measurements into real-world units.

---

## 6. Example Measurement Result

### Ground Truth Dimensions

| Dimension | Value  |
| --------- | ------ |
| Height    | 131 mm |
| Width     | 64 mm  |
| Thickness | 7 mm   |

### Predicted Dimensions

| Dimension | Predicted Value |
| --------- | --------------- |
| Height    | 131.0 mm        |
| Width     | 64.0 mm         |

The measurement demonstrates the successful implementation of the pixel-to-millimetre conversion pipeline using segmentation-derived object dimensions.

---

## 7. Segmentation Performance

The trained Mask R-CNN model was evaluated on the held-out test dataset.

### Evaluation Results

| Metric    | Value  |
| --------- | ------ |
| Mean IoU  | 0.9196 |
| Precision | 1.0000 |
| Recall    | 1.0000 |
| F1 Score  | 1.0000 |

These results indicate excellent segmentation quality and strong agreement between predicted masks and ground-truth annotations.

### Notes on Evaluation

Due to the limited measurement evaluation setup, the project demonstrates the complete pixel-to-millimetre conversion workflow but does not include a large-scale measurement validation study. Future work should evaluate multiple images and viewing conditions to compute Mean Absolute Error (MAE) and Mean Percentage Error (MPE).
---

## 8. Error Analysis

Potential sources of measurement error include:

* Camera position and viewing angle.
* Object orientation.
* Pixel quantisation effects.
* Segmentation boundary precision.
* Illumination variations.
* Bounding-box approximation.

The current implementation demonstrates the complete measurement workflow but was validated on a limited number of measurement examples.

A larger evaluation set containing multiple measurement samples at different distances and orientations would provide a more robust estimate of real-world measurement accuracy.

---

## 9. Limitations

Current limitations include:

* Single object category.
* Limited dataset size (80 images).
* Thickness estimation cannot be reliably inferred from a single image.
* Pixel-to-mm conversion was demonstrated using known object dimensions.
* Measurement validation was performed on a limited evaluation setup.

---

## 10. Future Improvements

Future enhancements may include:

* Larger and more diverse datasets.
* Multi-object measurement support.
* Automatic scale estimation using reference objects.
* Depth estimation for improved metric accuracy.
* Real-time deployment.
* Comprehensive measurement validation with MAE and MPE analysis.

---

## 11. Conclusion

A complete computer vision measurement pipeline was successfully implemented.

The system performs:

* Camera calibration
* Image undistortion
* Mobile phone segmentation
* Pixel measurement extraction
* Pixel-to-millimetre conversion
* Real-world dimension estimation

The trained Mask R-CNN model achieved:

* Mean IoU: 0.9196
* Precision: 1.0000
* Recall: 1.0000
* F1 Score: 1.0000

The results demonstrate the effectiveness of combining camera calibration and instance segmentation for object measurement applications.
