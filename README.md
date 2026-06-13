# Mobile Phone Segmentation and Dimension Measurement

## Project Overview

This project implements a complete computer vision pipeline for mobile phone segmentation and dimension estimation using camera calibration and Mask R-CNN.

The workflow includes:

1. Camera Calibration
2. Dataset Collection
3. Dataset Annotation
4. Instance Segmentation using Mask R-CNN
5. Model Evaluation
6. Real-World Dimension Measurement

## Object

* Device: iPhone 12 Mini

## Dataset

* Total Images: 80
* Training Images: 56
* Validation Images: 16
* Testing Images: 8
* Annotation Format: COCO Segmentation

## Camera Calibration

Checkerboard Calibration Pattern:

* 11 squares × 7 squares
* Square Size: 20 mm

Calibration Results:

* Successful Detections: 25/25
* Mean Reprojection Error: 0.2377

## Model

Architecture:

* Mask R-CNN
* ResNet50-FPN Backbone

Training Parameters:

* Optimizer: Adam
* Learning Rate: 0.0001
* Epochs: 10
* Batch Size: 2

Training Results:

* Final Train Loss: 0.0720
* Final Validation Loss: 0.1972

## Ground Truth Measurements

* Height: 131 mm
* Width: 64 mm
* Thickness: 7 mm

## Repository Structure

* notebooks/
* calibration/
* dataset/
* docs/
* models/
* outputs/
* reports/


