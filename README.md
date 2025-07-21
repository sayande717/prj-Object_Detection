# prj-Object_Detection
A Machine Learning based project for object detection. The target is to create a model that can be used in the field of Train Collision Avoidance.

## Workflow
1. **Obtain Dataset** from Roboflow using the Roboflow API.
2. **Preprocess Dataset**:
   1. Auto-orient using Pillow Image Manipulation Library.
   2. Resize images to 640*640, to make them suitable for YOLOv12.
   3. Normalize images in the range 0-1.
3. **Split Dataset**:
   1. Training: 72%
   2. Validation: 19%
   3. Test: 9%
4. **TRAIN MODEL: Implement Hybrid YOLOv12**
   1. Extract Initial features using standard (YOLO) method.
   2. Get the intermediate Feature Maps.
   3. Run 2 branches: main & sub:
      1. Main Branch: standard YOLOv12 processing
      2. Sub branch: CNN
         1. Feature Extraction
         2. Convolution & Pooling
         3. Get Feature Maps
   4. Combine the Feature Maps into the YOLO Detection Head. Accept Fused Features to produce:
      1. Bounding Box Coordinates
      2. Object class probabilities.
      3. Evaluation Metrics / Parameters.
   5. Use Confidence Threshold (0.35 - 0.75) to Remove Overlapping & Duplication Detections
   6. Based on threshold, Identify Ambiguities
   7. Extract Regions of Interest (RoI).
5. **TRAIN MODEL: Implement Post-YOLO MLP Classifier.**
   1. Extract RoI for classifier.
   2. Forward Pass using MLP Classifier (standard design)
   3. Gather Results (Confidence Score, Classification Probabilities, etc.)
6. **Combine Results**
   1. Get high-confidence outputs from `Hybrid YOLOv12`.
   2. Get Ambiguous Detections from `MLP Classifier`.
   3. Aggregate them to product the final result for the proposed model.
7. **TEST MODEL**: Display Annotated Images (2-3).

### Note: This is a work in progress.