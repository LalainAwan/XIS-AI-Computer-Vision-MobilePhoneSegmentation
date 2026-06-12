# Camera Calibration Report

## Calibration Setup

Camera: iPhone 15 Rear Camera (1×)

Checkerboard Pattern: 10 × 6 inner corners

Checkerboard Squares: 11 × 7

Square Size: 20 mm × 20 mm

Calibration Images Used: 25

Successful Detections: 25/25

---

## Camera Matrix

[[991.74437963, 0.0, 480.63190786],
 [0.0, 990.40810618, 635.13479258],
 [0.0, 0.0, 1.0]]

---

## Distortion Coefficients

[0.13358956,
 -0.71659962,
 -0.00164142,
 -0.00141431,
 0.57535074]

---

## Reprojection Error

0.2377 pixels

---

## Conclusion

The calibration achieved a reprojection error below 0.3 pixels, indicating excellent calibration accuracy. All subsequent measurements will use undistorted images generated from these intrinsic parameters.
