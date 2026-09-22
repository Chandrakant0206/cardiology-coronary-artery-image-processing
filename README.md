
# Cardiology Coronary Artery Image Processing

## Project Overview

This project processes cardiology X-ray/cine images to improve the visibility
of contrast-filled coronary arteries while suppressing unwanted anatomical
background structures.

The system supports 16-bit grayscale images and uses image preprocessing,
INT8 U-Net coronary vessel segmentation, rib/background suppression,
spine-region suppression, background suppression, and coronary artery
enhancement.

## Objective

- Process cardiology X-ray/cine images
- Support 16-bit grayscale input
- Suppress background noise
- Suppress rib/linear background structures
- Suppress central spine/background structures
- Suppress non-vessel lung/background structures
- Detect coronary vessels
- Enhance coronary artery visibility
- Preserve detected coronary vessel information
- Compare original, processed and enhanced images
- Achieve real-time processing performance

## Dataset

The project uses coronary artery image data with corresponding annotations
for training and evaluation.

The dataset was processed into image and vessel-mask pairs for coronary
artery segmentation.

## Model

The project uses a U-Net based coronary vessel segmentation model.

An INT8 TensorFlow Lite version of the trained model is used in the final
processing pipeline for faster inference.

## Processing Pipeline

The final processing pipeline is:

1. 16-bit grayscale input
2. 16-bit normalization
3. Gaussian noise suppression
4. CLAHE contrast enhancement
5. Image resizing
6. INT8 U-Net coronary vessel segmentation
7. Coronary vessel mask generation
8. Morphological vessel-mask cleaning
9. Rib/linear background structure detection
10. Rib suppression outside detected coronary vessels
11. Non-vessel background suppression
12. Central spine/background suppression
13. Coronary artery extraction
14. Final CLAHE coronary enhancement
15. Final enhanced coronary artery output

## 16-bit Image Support

The pipeline supports uint16 grayscale cardiology images.

The 16-bit input is normalized and prepared before the image-processing
and segmentation stages.

16-bit pipeline verification was successfully completed.

## Noise Suppression

Gaussian filtering with a 3x3 kernel is applied during preprocessing to
reduce image noise while maintaining coronary vessel structures.

## Rib Suppression

Elongated horizontal and vertical background structures are detected using
morphological operations.

Rib-like background structures are suppressed outside the predicted
coronary vessel mask so that detected coronary arteries are preserved.

## Spine Suppression

A central spine/background suppression region is applied to the image.

The suppression is restricted to non-vessel regions so that predicted
coronary vessels are preserved.

## Lung / General Background Suppression

The predicted coronary vessel mask is used to retain coronary vessel
regions while suppressing non-vessel anatomical background structures.

This provides suppression of lung and other non-vessel background regions
without requiring a separate lung segmentation model.

## Coronary Artery Enhancement

CLAHE-based local contrast enhancement is applied to improve the visibility
of the detected coronary artery structures.

Only detected coronary vessel regions are retained in the final enhanced
coronary output.

## Model Evaluation

Dice Score: 0.7538

IoU: 0.6048

Precision: 0.7854

Recall: 0.7245

Specificity: 0.9924

## Final Performance

Minimum Latency: 14.89 ms

Average Latency: 17.01 ms

Maximum Latency: 30.70 ms

P95 Latency: 22.45 ms

FPS: 58.78

Maximum permitted latency: 36 ms per frame

Result: PASSED

## Hardware Configuration

Operating System: Windows 10

CPU Cores: 4

Logical CPUs: 8

RAM: 7.24 GB

GPU: Not Available

## Software Environment

Python: 3.10.19

TensorFlow: 2.20.0

OpenCV: 4.13.0

## Output

The project provides:

1. Original 16-bit cardiology image
2. Noise-suppressed image
3. Coronary vessel mask
4. Background-structure suppressed image
5. Spine suppression mask
6. Final enhanced coronary artery image
7. Latency benchmark results

## Original / Processed / Enhanced Comparison

The system provides visual comparison of:

- Original/Raw cardiology image
- Processed image
- Enhanced coronary artery image

## Project Structure

Cardiology-Coronary-Artery-Image-Processing/

    Cardiology_Coronary_Artery_Image_Processing.ipynb
    README.md
    requirements.txt
    models/
    data/
    outputs/
    results/

## Installation

Install the required Python packages using:

pip install -r requirements.txt

## Usage

1. Open the project notebook.
2. Install the required packages.
3. Load the cardiology image.
4. Prepare the 16-bit grayscale input.
5. Run preprocessing.
6. Run the INT8 U-Net segmentation.
7. Generate the coronary vessel mask.
8. Apply rib/background suppression.
9. Apply spine/background suppression.
10. Extract and enhance coronary arteries.
11. View the original, processed and enhanced outputs.
12. Run the latency benchmark.

## Performance Summary

The final processing pipeline achieved:

Average latency: 17.01 ms

Maximum latency: 30.70 ms

FPS: 58.78

The maximum permitted processing latency is 36 ms per frame.

The measured maximum latency of 30.70 ms is within the required limit.

## Conclusion

The implemented pipeline supports 16-bit cardiology image processing,
noise suppression, rib/linear background suppression, spine/background
suppression, non-vessel lung/background suppression, coronary vessel
segmentation, and coronary artery enhancement.

The final latency benchmark demonstrates that the complete processing
pipeline operates within the required 36 ms per-frame limit.
