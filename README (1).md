# Tissue Segmentation Project - README

**Authors:** [Your Name(s)]

**Project Name:** Tissue Segmentation Project

**Final Project Date:** [Date]

---

## Introduction

The Tissue Segmentation Project is a critical endeavor focused on segmenting brain tissue from medical images. This process involves the partitioning of brain images into distinct regions or tissue types, including gray matter (GM), white matter (WM), and cerebrospinal fluid (CSF). Accurate tissue segmentation is pivotal in the diagnosis of various brain disorders, such as brain tumors, stroke, and brain atrophy.

In this project, we harnessed the power of the UNet architecture, a highly effective tool known for its outstanding performance in brain tissue segmentation across diverse imaging datasets. Our project revolves around the MICCAI Grand Challenge of MR Brain Image Segmentation, where the primary objective is to segment T1 brain images into CSF, GM, and WM.

## Methodology

### Dataset

We utilized the IBSR (Intensive Care Unit Normalized Brain MRI Database) dataset, which consists of 18 T1-weighted MRI scans of the brain, each accompanied by manual segmentations of GM, WM, and CSF. We meticulously divided this dataset into ten volumes for training, five for validation, and three for testing.

### Implementation

#### Preprocessing

Our journey commenced with thorough preprocessing to address variations in image intensities and eradicate background noise. To ensure data consistency, we normalized the images to achieve a mean of 0 and a standard deviation of 1. Negative values were appropriately adjusted to a minimum of 0.

#### Region of Interest (ROI)

To concentrate our efforts on pertinent image regions, we meticulously calculated Regions of Interest (ROIs) before commencing training. This process enabled us to efficiently extract and eliminate background elements and irrelevant slices from the images, leaving us solely with areas of genuine interest.

#### Patches Extraction

To facilitate efficient processing, we dissected the images into smaller patches, each measuring either 32x32x32 or 16x16x16 in size. To ensure uniformity, we introduced zero-padding. To avoid processing irrelevant data, we thoughtfully designed a function to extract patches containing pertinent information while discarding those dominated by background.

#### Loss Function

In our pursuit of precision, we adopted a multi-loss approach for our loss function. By combining the cross-entropy and Dice coefficient loss functions, we gained the flexibility to assign varying weights to these loss functions, guided by a threshold of 0.65.

#### Network

Recognizing the risk of overfitting, especially with a limited training dataset, we introduced crucial elements to our convolutional neural network (CNN). These elements include batch normalization and dropout (dropout rate: 0.2). To ensure proper normalization, we employed instance normalization.

#### Experimentation

Our model underwent rigorous training for a total of 100 epochs, supported by an early stopping mechanism. This mechanism halted training if the validation loss displayed no improvement for 20 consecutive epochs. Additionally, we engaged in experiments involving multiple batch sizes (ranging from 16 to 32) and patch sizes to fine-tune our model's performance.

### Parameter Optimization

| Parameter                | Patch Size | Batch Size | Optimizer | Dropout | Training Scheduler |
|--------------------------|------------|------------|-----------|---------|--------------------|
| Experiment 1   | 32x32x32   | 32         | ADAM      | 0.2     | None, 10, 20       | 
| Experiment 2   | 16x16x16   | 64         | ADAM      | 0.2     | None, 10, 20       | 

## Conclusion

Through diligent efforts, we have successfully engineered a 3D UNet-based brain tissue segmentation model utilizing the IBSR dataset. Our carefully selected parameters have consistently demonstrated high validation accuracy, positioning our model as a promising candidate for extensive testing and evaluation.

---

**Instructions for Running the Code**

1. clone the repository 
2. download the data set from https://www.nitrc.org/projects/ibsr