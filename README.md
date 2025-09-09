1. Introduction

Agriculture is the backbone of many economies, but crop yield is heavily affected by plant diseases. Traditionally, farmers detect diseases by manual inspection, which is time-consuming, requires expertise, and often leads to delayed action.

👉 Deep Learning + Computer Vision helps automate this process:

Farmers can capture leaf images using smartphones or drones.

A trained CNN model classifies whether the plant is healthy or diseased, and if diseased, identifies the type of disease.

2. Dataset

The most widely used dataset is PlantVillage (≈ 54,000+ labeled images, 38 categories).

Images are categorized by crop type (e.g., tomato, potato, maize) and disease type (e.g., early blight, late blight, rust).

Classes are structured as folders:


3. Preprocessing Pipeline

Resize images to a fixed size (e.g., 224×224).

Normalize pixels (0–1 or using pretrained model’s preprocessing).


4. Model Architectures
🔹 (A) From Scratch CNN (educational, but less accurate)

Conv2D → MaxPooling → Conv2D → Flatten → Dense → Output

Works only if dataset is huge.

🔹 (B) Transfer Learning (recommended)

Use pretrained models (MobileNet, EfficientNet, ResNet) trained on ImageNet.

Replace the top layer with your own classifier (Dense(num_classes, softmax)).

Freeze pretrained layers initially, then fine-tune last few layers.


5. Training

Loss: categorical_crossentropy (multi-class).

Optimizer: Adam or SGD with momentum.

Metrics: Accuracy, F1-score (important in imbalanced classes).

Callbacks:

EarlyStopping → stop training if validation loss doesn’t improve.

ReduceLROnPlateau → lower learning rate on plateau.

ModelCheckpoint → save best weights.

6. Evaluation Metrics

Accuracy → overall performance.

Precision & Recall → important if some diseases are rarer.

Confusion Matrix → shows per-class performance.

F1 Score → balances precision & recall.



7. Model Explainability

Deep models are black boxes. To build trust:

Use Grad-CAM to visualize which parts of the leaf influenced the decision.

Helps ensure the model focuses on the leaf, not background.

8. Model Saving and Deployment

In Keras 3, saving/exporting changed:

For re-training/reloading:

Augmentation (flip, rotate, zoom, color jitter) to improve generalization.

Batching & Prefetching for efficient training.
