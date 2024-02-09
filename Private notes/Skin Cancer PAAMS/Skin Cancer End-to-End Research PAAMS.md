---
share: true
path: 'Private notes/Skin Cancer PAAMS'
attachment:
  send: true
  folder: 'Private notes/Skin Cancer PAAMS/assets'
---
# Dataset

This data information can be seen here:
- https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/DBW86T
- https://www.kaggle.com/datasets/kmader/skin-cancer-mnist-ham10000/data

## Description

This dataset consists of 10015 dermatoscopic images. Cases include a representative collection of all important diagnostic categories in the realm of pigmented lesions: Actinic keratoses and intraepithelial carcinoma / Bowen's disease (`akiec`), basal cell carcinoma (`bcc`), benign keratosis-like lesions (solar lentigines / seborrheic keratoses and lichen-planus like keratoses, `bkl`), dermatofibroma (`df`), melanoma (`mel`), melanocytic nevi (`nv`) and vascular lesions (angiomas, angiokeratomas, pyogenic granulomas and hemorrhage, `vasc`).

More than 50% of lesions are confirmed through histopathology (`histo`), the ground truth for the rest of the cases is either follow-up examination (`follow_up`), expert consensus (`consensus`), or confirmation by in-vivo confocal microscopy (`confocal`). The dataset includes lesions with multiple images, which can be tracked by the `lesion_id`-column within the **HAM10000_metadata** file.

---

## Additional data for evaluation purposes

The HAM10000 dataset served as the training set for the [ISIC 2018 challenge (Task 3)](http://arxiv.org/abs/1902.03368), with the same sources contributing the majority of the validation- and test-set as well. The test-set images are available herein as **ISIC2018_Task3_Test_Images.zip (1511 images)**, the ground-truth in the same format as the HAM10000 data (public since 2023) is available as **ISIC2018_Task3_Test_GroundTruth.csv**.
	We should use the ISIC2018_Task3_Test_Images for the final validation of model and to measure the ability to generalize.

<ins>I made all of this data available at: </ins> 

---
# Brief Literature Review

## What was done for us before 

https://www.kaggle.com/code/franciscomesquita/ad-tp1-skin-lesions-images-classification or https://github.com/Francisc17/Skin-Disease-Image-Classification-With-CNNs/blob/main/ad-tp1-skin-lesions-images-classification.ipynb

**Logic behind the choice of every article below:** Articles that cite this data and work on it for the same purpose that we want to: Classify the skin lesion type. 
## Classification of Skin Lesions from Dermatoscopic Images Using Convolutional Neural Networks by Oniga et al. [DOI 10.1109/CSCS59211.2023.00044](https://ieeexplore.ieee.org/document/10214735)

**Methodology diagram**

![500](assets/Skin%20Cancer%20End-to-End%20Research%20PAAMS%20-%20methodology%20oniga.png)


**Imbalance problem:**

From the original distribution:
![600](assets/Skin%20Cancer%20End-to-End%20Research%20PAAMS%20-%20original%20distribution%20oniga.png)

They created a new one dataset which contains aproximately equal number of images from each of the seven classes. To make these, authors use image augmentation. The final data looks like this:
![600](assets/Skin%20Cancer%20End-to-End%20Research%20PAAMS%20-%20new%20data%20balance%20oniga.png)

**Models tested:**
1. ResNet
2. DenseNet
3. GoogLeNet
4. VGG16
5. MobileNetV2

**Results**

Training:
![600](assets/Skin%20Cancer%20End-to-End%20Research%20PAAMS%20-%20training%20results%20oniga.png)

Test:
![600](assets/Skin%20Cancer%20End-to-End%20Research%20PAAMS%20-%20test%20results%20oniga.png)

Per class:
![400](assets/Skin%20Cancer%20End-to-End%20Research%20PAAMS%20-%20per%20class%20result%20oniga.png)

**Output Interpretation:**
Not presented

**Deployment:**
Not presented

---

## On the Automatic Detection and Classification of Skin Cancer Using Deep Transfer Learning by Fraiwan et al. https://doi.org/10.3390/s22134963

**Methodology diagram:**
![700](assets/Skin%20Cancer%20End-to-End%20Research%20PAAMS%20-%20methodology%20fraiwan.png)

**Imbalance problem:**
Authors do not balance data

**Models tested**
1. SqueezeNet
2. GoogLeNet
3. InceptionV3
4. DenseNet201
5. MobileNetv2
6. Resnet101
7. Resnet50
8. Resnet18
9. Xception
10. Inception
11. ResNetV2
12. ShuffleNet
13. DarkNet-53
14. EfficientNetb0

**Results:**
![700](assets/Skin%20Cancer%20End-to-End%20Research%20PAAMS%20-%20results%20fraiwan.png)

**Interpretation:**
Not presented

**Deploy:**
Not presented

---
## Is it Time to Replace CNNs with Transformers for Medical Images? by Matsoukas et al. [https://doi.org/10.48550/arXiv.2108.09038](https://doi.org/10.48550/arXiv.2108.09038)

**Methodology diagram:**
Not presented

**Imbalance problem:**
Authors do not balance data

**Models tested:**
1. ResNet50
2. DeiT-S (ViT)

**Results:**
![800](assets/Skin%20Cancer%20End-to-End%20Research%20PAAMS%20-%20results%20matsoukas.png)

**Interpretability:**
Authors use Grad-CAM only.

**Deployment:**
Not presented

---
## Multiclass skin cancer classification using EfficientNets – a first step towards preventing skin cancer by Karar Ali https://doi.org/10.1016/j.neuri.2021.100034

**Methodology used:**
An image is not presented but it can be explained with the following steps:
1. Class wise distribution (split train / val / test per class)
2. Remove hair on some image to reduce noise
3. They increase dataset using augmentation techniques (zooming, horizontal and vertical flipping). I could not understand how the distribution is after this step...

**Imbalance problem:**
Although authors used augmentation, i think that they did not change the target distribution.

**Models tested:**
- All EfficientNet variation from EfficientNetb0 to EfficientNetb7

**Results:**

Best model was EfficientNetb4
![400](assets/Skin%20Cancer%20End-to-End%20Research%20PAAMS%20-%20results%20ali.png)

![900](assets/Skin%20Cancer%20End-to-End%20Research%20PAAMS%20-%20comparation%20ali.png)

**Interpretation:**
Not presented

**Deployment:**
Not presented

---

## Dermatologist-like explainable AI enhances trust and confidence in diagnosing melanoma by Chanda et al. https://doi.org/10.1038/s41467-023-43095-4

to be continued...