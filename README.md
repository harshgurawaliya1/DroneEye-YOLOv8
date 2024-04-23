# DroneEye-YOLOv8
YOLOv8 Custom Training for Aerial Personal Identification

This repository contains the training pipeline for a custom YOLOv8 model designed for identifying individuals from aerial drone footage, with a special focus on two subjects: 'Jai' and 'Harsh'. The model was trained using a modified YOLOv8 large (yolov8l) architecture for enhanced detection precision in complex environments.
youtube video link : https://youtu.be/m8ZwA6-17xQ?si=kbDPogQdSrE7BxpU
![Screenshot 2024-04-14 033431](https://github.com/harshgurawaliya1/DroneEye-YOLOv8/assets/106898396/809af247-e050-4bca-8904-12ac6fd094e4)

Training Configuration

Model: YOLOv8 large (yolov8l) pre-trained on a general dataset.

Dataset Path: /kaggle/working/datasets/drone-final-1/data.yaml.

Epochs: 500, with early stopping if no improvement in 50 epochs.

Batch Size: 16 images to balance between memory usage and convergence speed.

Image Size: 800x800 pixels, chosen for optimal detail resolution.

Optimizer: Auto-detected best optimizer (likely AdamW) with a learning rate of 0.001667, momentum of 0.9, and weight decay of 0.0005.

Hardware: Tesla P100-PCIE-16GB, leveraging CUDA for efficient computation.


Model Summary
The YOLOv8 large model used contains 365 layers with over 43 million parameters, adapted to detect 2 classes, significantly reducing from the original 80 classes. This focused the model's learning capacity on distinguishing between the two subjects, 'Jai' and 'Harsh'.

Training Progress

Training progress was closely monitored through a range of metrics:

Box Loss: Measures how well the model predicts the location of the bounding boxes.

Class Loss: Represents the error in predicting the correct class out of the two possible.

DFL Loss: The 'Distribution-Focal Loss' unique to YOLOv8, focusing on hard examples.

Improvements were seen as the box loss and class loss steadily decreased, while the mAP50 metric (mean Average Precision at 50% IoU) remained high, indicating strong predictive performance.
![Screenshot 2024-04-14 030011](https://github.com/harshgurawaliya1/DroneEye-YOLOv8/assets/106898396/466e8d27-0a76-4c07-baa3-aee5d2c8b838)
![Screenshot 2024-04-14 041215](https://github.com/harshgurawaliya1/DroneEye-YOLOv8/assets/106898396/e6ec8458-8fdf-4de9-974e-fde82336fafe)

Early Stopping

To prevent overfitting and ensure computational efficiency, training incorporated early stopping. The best model was saved at epoch 84 when peak performance was detected, halting further training after no improvements were observed in subsequent epochs.

Validation Results

Post-training validation was conducted, yielding high precision and recall rates. The mAP50 for class 'jai' and overall remained high, which underscores the model's accuracy.
![Screenshot 2024-04-14 030552](https://github.com/harshgurawaliya1/DroneEye-YOLOv8/assets/106898396/cd6ad186-1282-4615-bb67-f84b6161d616)

Deployment
The final model (best.pt) is stripped of the optimizer for deployment, resulting in a lightweight file ready for real-time inference tasks.

Usage
For detection, run the inference script using the provided weights on your target drone footage. The inference speed and high accuracy make it suitable for real-time applications.
