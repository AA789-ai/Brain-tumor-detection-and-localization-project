# Tumor Detection and Localisation project

# Important: All usefuls images can be found in MRI.ipynb file

This project aim to scan brain MRIs to determine if a patient has a brain tumor or not. If the patient has a brain tumor, it localizes the brian tumor. We also make use of transfer learning to improve and speed up our model training.

The model employs deep learning to build 2 models:
  1. ResNet-50 model for classfication
  2. Custom ResUNet model for segmentation.

The dataset contains approximately 4000 MRI scans in which 2550 don't have any tumor and nearly 1350 have brain tumor. 

**_Dataset source_** : https://www.kaggle.com/datasets/mateuszbuda/lgg-mri-segmentation

The project can be divided into the following parts:

#### Common steps

  1. **Loading Data:** This part consists of get some information about the dataset.
  2. **Visualising Data:** This part of the dataset, we show the number of scans with tumor and number of scans without tumor. To show the tumor, we show a scan along with its tumor on a separate plotted graph with same dimensions to indicate where the image needs to be. We then combine these two images to show where the tumor is located on the MRI scan.
  3. **Data preprocessing:** This section consists of cleaning, splitting and augmenting our database.

#### Steps specific to model #1: ResNet-50 for classification

  5. **Building a Classfication Model using ResNet-50:** We used transfer learning to build our model. We base ourself on ResNet-50 trained model on imagenet dataset which contains over 14 millions images in high resolution. We then tailor the model to our own needs for MRI scan classification.
  6. **Compiling And Training:** This parts consists of training the model, saving the best model, as well as its architecture.
  7. **Assess the model 1's performance:** We were able to achieve  nearly 98% accuracy when it comes to predicting whether a patient has a brain tumor or not based on the brain's MRI scan.

#### Steps specific to model #2: Custom ResUNet model for segmentation
  8. **Second Deep Learning Model - Building a segmentation model:** We built a ResUnet model with some alterations. We define our own resnet block and function to upscale and concatenate.
  9. **Compiling And Training:** This parts consists of training the model, saving the best model, as well as its architecture.
  10. **Assess the model 2's performance:** In order to assess, we provided 5 images:
      a. Brain MRI
      b. Original Mask: this corresponds to the actual tumor.
      c. Predicted Mask: this corresponds to the tumor predicted by our model.
      d. Brain MRI with Original Mask: This image combines the MRI and the brain tumor which is colored in red.
      e. MRI with AI predicted Mask: This image combines the MRI scan and the brain tumor which is colored in green.

Here are some some sample images:
![image](https://github.com/AA789-ai/TumorDetection/assets/97749196/2281e5bf-5bdc-4cf1-9f59-823604cae59a)

As we can see, our model's ability to localize tumors is very similar to the actual tumor. For more details, please feel free to visit my MRI.ipynb file.

