# Leaf Image Processing & Classification Pipeline in Matlab🍃🤖

This repository implements a complete pipeline for processing leaf images—from segmentation to classification—designed to work with compositions containing multiple leaves or unknown objects. Below is a breakdown of the modules and their functionalities:

---

## Classifier Module 🎯

- **File:** classifier.m`  
- **Purpose:**  
  - Extracts image features and trains the classifier.
  - The features to be extracted are defined in the `setup.m` file.
- **Features Used for Classification:**  
  - **Color-Based Features:**  
    - Quantized HSV histograms  
    - Advanced statistical moments (mean and standard deviation for hue, saturation, and value)  
    - Composite measures like colorfulness, dominant hue analysis, and saturation-value energy  
  - **Additional Features:**  
    - Contour Fourier descriptors (using `extractContourFourier`)
    - Edge features (using `extractEdge`)
    - Eccentricity (using `extractEccentricity`)
    - Aspect ratio (using `extractAspectRatio`)
- **Output:**  
  - The classifier assigns each extracted leaf to one of 10 classes (Plant 1 to Plant 10)

---

## Localizer Module 🔍

- **File:** `segmentation.m`  
- **Purpose:**  
  - Generates mosaics to train the localizer, which is responsible for accurately segmenting leaves from compositions.
- **Segmentation Process:**  
  1. **Enhancement:**  
     - An enhancement step is first applied to improve image quality.
  2. **Edge Detection:**  
     - Utilizes a combination of the Sobel operator and a Canny's algorithm to extract precise edge information.
  3. **Mask Combination:**  
     - The edge-derived mask is merged with the segmentation result from the localizer, which is based on a Random Forest model.
- **Color Spaces Utilized:**  
  - RGB, HSV, YCbCr, ExG, ExR, and LAB are used to derive comprehensive segmentation features.
- **Evaluation:**  
  - The module predicts a mask for each composition and then calculates accuracy by comparing these masks against ground truth data.
- **What is the Localizer?**  
  - The localizer is a specialized module aimed at pinpointing the exact location of leaves within an image.

---

## Main Application 🚀

- **File:** `main.m`  
- **Purpose:**  
  - Serves as the central application that integrates the segmentation and classification pipelines.
  - Processes a given composition by:
    - Extracting the enhanced segmentation mask.
    - Classifying each individual leaf or unknown object present.
- **Workflow:**  
  1. **Input:** A composition image.
  2. **Segmentation:** Uses the localizer and enhanced edge detection to obtain a refined mask.
  3. **Classification:** Feeds segmented leaves into the classifier to determine the plant category and confidence level.
        - **Certain** (high confidence)
        - **Uncertain** (some ambiguity)
        - **Unknown** (object not matching any known class)
---

Example Detection Result 🖼️
Below is an example of the leaf segmentation and classification output produced by this pipeline:

<p align="center"> <img src="src/detection_example.png" alt="Example of leaf segmentation and classification" width="550"/> </p>
The image above shows a typical result: segmented leaves are outlined and assigned their predicted classes. “Unknown” objects are handled robustly, ensuring versatility across diverse compositions.



This project combines advanced image processing techniques with robust machine learning models to offer a versatile solution for leaf segmentation and classification. Whether you're working on precision agriculture, botanical research, or image recognition, this repository provides a solid foundation and clear modular design. 
🌿✨
