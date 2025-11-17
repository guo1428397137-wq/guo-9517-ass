# 9517
# 这里是25T3，9517-group176小组作业上传空间，大家写完之后上传就可以了
This project implements a classical computer vision–based object detection and classification system using HOG features, Random Forest classifiers, and Selective Search for region proposals.
Models
Two Random Forest models were trained:
Whole-image classification model
Trained using entire training images
Evaluates classification performance on whole images
Not used during object detection

Region-based classification model
Trained on insect regions cropped using YOLO bounding boxes
Used during detection to classify region proposals

Detection Pipeline
Input a test image
Apply Selective Search to produce region proposals
For each proposed region:
Resize → convert to grayscale
Extract HOG features
Classify with the region-based RF model
Filter overlapping proposals using Non-Maximum Suppression (NMS)
Output final bounding boxes and insect class predictions
Evaluate performance using mAP and per-class AP

Results and Analysis
Detection Performance
Mean Average Precision (mAP): 0.0038
Highest class AP: Moths (0.0067)
Likely due to their relatively consistent shape and texture, which fit well with HOG descriptors
Whole-image Classification Performance
Macro Precision: 0.2216
Macro Recall: 0.2261
Macro F1-score: 0.2045
Shows that classical features struggle with global image classification
Per-class Observations
Best detection: Moths (F1 = 0.4783, AUC = 0.834)
Worst detection: Beetles (F1 = 0.0000, AUC = 0.503)
Classes with distinct texture/patterns (e.g., Moths, Snails) perform better than those with subtle or variable features

Conclusion
The HOG + Random Forest pipeline demonstrates that classical CV methods can perform basic object detection. While suitable for simple textures, their performance on complex scenes is limited compared to CNN-based approaches.
