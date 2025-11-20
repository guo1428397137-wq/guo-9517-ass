The goal of this project is to detect insects using a deep learning model. The dataset contains 12 insect categories. I chose PyTorch's built-in Faster R-CNN (ResNet50 + FPN). This is a typical two-stage object detection model with advantages such as high detection accuracy and relatively good performance for small objects, theoretically very suitable for detecting small objects such as insects. My task is to input this information into Faster R-CNN to train the model to detect insects in images and determine their categories.



The training settings are as follows: batch size of 4, initial learning rate of 0.002, and epochs of 20. I used StepLR to gradually reduce the learning rate from 0.002 to 0.0002, and then to 0.00002, and used AMP (Analog Precision Mixed Model) and gradient pruning to ensure training stability. To avoid training anomalies, I created a label reading function to handle empty text files, out-of-bounds boxes, and invalid boxes. I also mapped each YOLO category (0-11) according to PyTorch's requirement of "1-12 + 0 background". In addition, I created the dataset itself: an automatically scanned folder of images, matching files with their corresponding labels, zooming in on the data, scaling it to 800 along its longest side, and synchronously scaling the bounding box coordinates before normalization.



Looking at the training logs, we can see the loss curve drop from about 1.8 to about 0.9 in the first few runs, then fluctuate around 1.5. However, the mAP remains almost constant, peaking at only 0.0002. This indicates that while the model reduced the loss, it didn't actually learn an effective detection method. Looking at the validation set reveals two extreme examples. At a very low threshold, all images are filled with numerous red boxes, most with low confidence and almost no overlap with the true green boxes. When we slightly increased the threshold, "Pred: 0" boxes appeared throughout the images, indicating that the model didn't actually learn the location and category of the bounding boxes. Possible reasons include: small errors in the YOLO to R-CNN coordinate transformation process may have corrupted the training data; insect targets are very small and of very similar categories, leading to incompatibility between default anchor boxes and hyperparameters; and the limited number of training iterations and lack of specific tuning for the learning rate and time.



Although the results are not ideal, I am still very satisfied with this project. If I want to continue improving it, I will prioritize testing simpler models, which may be better suited for handling small targets and complex backgrounds.



