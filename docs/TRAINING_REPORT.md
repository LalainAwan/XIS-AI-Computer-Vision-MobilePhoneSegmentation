# Training Report

## Model Selection

The selected model is Mask R-CNN with a ResNet50-FPN backbone.

This architecture was chosen because it provides instance segmentation masks, which are required for accurate object boundary extraction and dimensional analysis.

## Dataset

* Total Images: 80
* Training Images: 56
* Validation Images: 16
* Testing Images: 8

Class:

* mobile_phone

## Hyperparameters

* Optimizer: Adam
* Learning Rate: 0.0001
* Epochs: 10
* Batch Size: 2

## Results

Final Training Loss:
0.0720

Final Validation Loss:
0.1972

## Output Model

mask_rcnn_mobile_phone.pth

## Conclusion

The model successfully learned mobile phone segmentation and generated accurate object masks suitable for subsequent dimension estimation.
