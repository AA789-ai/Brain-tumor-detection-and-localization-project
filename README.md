# Tumor Detection and Localization Project

## Project Overview

A deep learning project designed to analyze brain MRI scans to detect and localize brain tumors with high accuracy. This solution combines classification and segmentation models to provide comprehensive diagnostic support for medical professionals. The system first determines if a tumor is present, then precisely identifies its location within the brain tissue.

## Key Features

* **Dual-Model Architecture:** Utilizes separate models for comprehensive analysis:
    * **Classification:** Detects the presence or absence of a tumor.
    * **Segmentation:** Precisely outlines the tumor's location and shape.
* **High Accuracy:** The classification model achieves **98% accuracy** in tumor detection.
* **Transfer Learning:** Employs a pre-trained ResNet-50 model (on ImageNet) for classification, improving training efficiency and performance.
* **Custom Segmentation Model:** Implements a tailored ResUNet architecture for accurate tumor localization.
* **Detailed Visualization:** Generates visual outputs showing the original MRI, the actual tumor mask (ground truth), the predicted tumor mask, and overlays of the masks onto the MRI for clear interpretation.
* **Modular Design:** Allows for potential future enhancements and integration with medical imaging systems.

## Technical Details

* **Frameworks/Libraries:** TensorFlow, Keras
* **Models:**
    * **Classification:** ResNet-50 (leveraging transfer learning)
    * **Segmentation:** Custom ResUNet architecture
* **Dataset:** LGG MRI Segmentation dataset from Kaggle (Link below)
* **Preprocessing:** Includes data cleaning, train/validation/test splitting, and data augmentation techniques.
* **Environment:** Developed and tested using Python.

## Dataset

* **Source:** [LGG MRI Segmentation Dataset on Kaggle](https://www.kaggle.com/datasets/mateuszbuda/lgg-mri-segmentation)
* **Composition:** Approximately 4,000 brain MRI scans.
    * ~2,550 scans without tumors (Healthy)
    * ~1,350 scans with tumors (Low-Grade Glioma)
* **Format:** Each tumor case includes the MRI scan and a corresponding segmentation mask indicating the tumor region.

## Methodology

The project workflow is divided into common preprocessing steps followed by specific steps for each model:

#### Common Steps
1.  **Data Loading:** Load MRI scans and corresponding masks (if applicable). Gather basic information about the dataset structure and size.
2.  **Data Visualization:** Analyze the distribution of tumor vs. non-tumor scans. Visualize sample MRI scans alongside their ground truth segmentation masks to understand the data. Overlay masks onto scans for better spatial understanding.
3.  **Data Preprocessing:**
    * Clean the data (handle missing values, inconsistencies if any).
    * Split the dataset into training, validation, and testing sets.
    * Apply data augmentation techniques (e.g., rotation, flipping) to increase dataset diversity and improve model robustness.

#### Model #1: ResNet-50 for Classification
4.  **Model Building:** Adapt a pre-trained ResNet-50 model (trained on ImageNet) for the binary classification task (tumor/no tumor). Replace the final layers to suit the specific needs of MRI scan classification.
5.  **Model Compilation & Training:** Compile the model with an appropriate optimizer (e.g., Adam), loss function (e.g., Binary Crossentropy), and metrics (e.g., Accuracy). Train the model on the preprocessed dataset, saving the best performing weights based on validation accuracy.
6.  **Performance Evaluation:** Assess the trained classification model on the test set. Key metric: Accuracy.

#### Model #2: Custom ResUNet for Segmentation
7.  **Model Building:** Construct a ResUNet model. This typically involves:
    * An encoder path (similar to ResNet) to capture context.
    * A decoder path to enable precise localization using up-sampling and concatenation with corresponding encoder feature maps.
    * Define custom ResNet blocks and up-sampling functions as needed.
8.  **Model Compilation & Training:** Compile the model using an appropriate optimizer, loss function suitable for segmentation (e.g., Dice Loss, Binary Crossentropy), and relevant metrics (e.g., Dice Coefficient, Intersection over Union - IoU). Train the model on the preprocessed dataset (scans and masks), saving the best performing model based on validation metrics.
9.  **Performance Evaluation:** Evaluate the segmentation model on the test set using metrics like Dice Coefficient or IoU. Visualize the results by comparing predicted masks against ground truth masks.

## Results

* **Classification:** The ResNet-50 based classification model achieved **~98% accuracy** in distinguishing between MRI scans with and without tumors on the test dataset.
* **Segmentation:** The custom ResUNet model effectively localizes tumors. Visual assessments demonstrate a high degree of overlap between the predicted masks and the ground truth masks.

* Classification Performance (Confusion Matrix):**
![Confusion Matrix for Tumor Classification](https://github.com/user-attachments/assets/68481455-a16e-4477-b590-62c1cfec3135)
*Confusion matrix for the tumor classification model (Tumor=1, No Tumor=0). Shows high accuracy (~97.7%) with low false positives (1) and few false negatives (12).*



**Sample Segmentation Output:**

The following image shows an example of the segmentation model's output:

![Sample Segmentation Result](https://github.com/AA789-ai/TumorDetection/assets/97749196/2281e5bf-5bdc-4cf1-9f59-823604cae59a)

*Example showing (a) Brain MRI, (b) Original Mask, (c) Predicted Mask by AI, (d) MRI with Original Mask overlay, (e) MRI with AI Predicted Mask overlay*

**Note:** Detailed visualizations, including comparisons between original and predicted masks overlaid on MRI scans for multiple examples, can be generated and viewed by running the `MRI.ipynb`
