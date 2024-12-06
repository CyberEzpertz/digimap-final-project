# Image Segmentation using Various Edge Detection Algorithms

This project explores image segmentation using various edge detection algorithms, namely **Canny**, **Sobel**, **Scharr**, and **Laplace** to separate the background and foreground of an image. Additionally, this project compares the algorithms in terms of performance with regards to masking an image's foreground.


## Overview

This project uses image segmentation functions from OpenCV's library in order to remove the backgrounds of images or blur them inside a Jupyter Notebook. This is done with the use of edge detection algorithms, whose results are then used to find the most significant top-level contour of the image. This contour is then used to create the mask that will be used to segment the image's background and foreground, either removing or blurring the former.

Performance was also measured across the four algorithms, measuring their average execution time, accuracy, specificity, and sensitivity. This was done with the help of ground truth masks, which were created using the background-removed dataset images created with the use of a 3rd-party image editing software. 

### Dataset Used
This project uses images from the following dataset from Kaggle:
[Selfies & ID Images Dataset](https://www.kaggle.com/datasets/tapakah68/selfies-id-images-dataset)

### Edge Detection Algorithms Used:
1. **Canny Edge Detector**: A multi-stage algorithm that detects a wide range of edges in images while minimizing noise.
2. **Sobel Operator**: A gradient-based method used to compute the approximation of the gradient of image intensity.
3. **Scharr Operator**: Similar to Sobel, but uses a different kernel for better edge detection.
4. **Laplacian Operator**: Detects edges by looking at regions where the intensity function changes rapidly.

### Other Algorithms Used
1. **Savitzky-Golay Filter** - A digital filter used to smoothen data points. This is used to smoothen the contours for the mask.

### General Algorithm Flow
The flow below is applied to every algorithm except Canny since it has a built-in RGB channel handler. 

![image](https://github.com/user-attachments/assets/87e815e0-9053-42b4-b4a0-ef1212e44ce4)


## Setup & Installation

Clone this repository to your local machine:

```sh
git clone https://github.com/CyberEzpertz/digimap-final-project.git
```

Once done, you will need to install the required libraries.

```sh
pip install requirements.txt
```

After, open up the [Final Project](final_project.ipynb) file and run all of the code blocks.

## Folder Structure
This project uses 2 folders for its input, with the rest being the outputs.

### Input Folders
- `dataset` - Contains the base images that will be used in the notebook.
- `correct_dataset` - Contains the images with their backgrounds removed through the use of a 3rd-party image editing software.

### Output Folders
- `blurred` - Contains the blurred background versions of the images.
- `masked` - Contains the removed background versions of the images.
- `resized` - Contains the resized versions of the images.

## Performance Metrics

### Machine Specifications

The entire project was ran on Deepnote's Basic Plan hardware. Unfortunately, the specific models on their hardware are undisclosed. [Here](https://deepnote.com/pricing) is the only information about their machines.
| **Part** | **Specification** |
| -------- | ----------------- |
| CPU | 2 vCPU |
| RAM | 5GB Memory | 

### Measured Values

To get the performance metrics for each algorithm, these values were first measured by comparing the result of the algorithm and the ground truth (cleaned) pictures. 

> [!NOTE]
> *Actual* in this context means the foreground & background in the ground truth picture.
 
- **True Positive** (TP) - Area of the actual foreground shown by the mask.
- **True Negative** (TN) - Area of the actual background covered by the mask.
- **False Positive** (FP) - Area of the actual background shown by the mask.
- **False Negative** (FN) - Area of the actual foreground covered by the mask.

These were then used in the calculation of the following metrics:

- **Average Execution Time** - Ave. time taken by the algorithm over the course of 20 images.
- **Accuracy** - Proportion of pixels correctly covered and shown by the mask. See equation below.
```math
\frac{TN + TP}{TN + TP + FP + FN}
```

- **Specificity** - Proportion of background pixels correctly covered by the mask. See equation below.
```math
\frac{TN}{TN + FP}
```

- **Sensitivity** - Proportion of foreground pixels correctly shown by the mask. See equation below.
```math
\frac{TP}{TP + FN}
```

### Analysis of Results

> [!NOTE]
> It is important to note that the execution times include the Sobel, Scharr, and Laplace running 3 times for each color channel, while Canny is only run once due to its innate ability to process RGB.

| **Algorithm** | **Accuracy (%)** | **Specificity (%)** | **Sensitivity (%)** | **Ave. Execution Time** |
|---------------|------------------:|---------------------:|---------------------:|-------------------------:|
| **Canny**     | 49.84%           | 43.06%              | 55.96%              | 2.76ms                  |
| **Sobel**     | 49.45%           | 42.04%              | 56.56%              | 3.97ms                  |
| **Scharr**    | 49.75%           | 42.15%              | 56.93%              | 5.38ms                 |
| **Laplace**   | 41.90%           | 24.48%              | 59.85%              | 1.12ms                  |

Based on these values, we can see that the Canny has the fastest time, highest accuracy, highest specificity, but it has the lowest sensitivity. On the other hand, Laplace has the lowest accuracy and specificity by a large margin, which indicates that its masking was the most inaccurate out of all, with the background being included in most of its results. However, it does have the highest sensitivity and fast execution time, so in essence, it is exchanging time for accuracy. 

Scharr has the longest execution time, however it consistenly comes in at second place in every other metric. Lastly, Sobel is third in all categories, being faster than Scharr, essentially trading time for accuracy once again, but not by a large margin.

Overall, these results indicate that it is possibly best to use Canny for quick and accurate results, while Laplace is unrecommended due to its quick but inaccurate results. If time is of no issue, Scharr or Sobel may possibly be considered due to their consistent performance.


## Contributors
This project was created with the joint effort of [S13] Digimap - Group 11.

**Members**
- **Caramat**, Christian Jude G.
- **Morales**, Alejandro Jose E.
- **Murillo**, Jan Anthony B.
- **Yap**, Rafael Subo A.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Code References
- [Background removal with OpenCV (AKA segmentation) - Munawwar Firoz](https://www.codepasta.com/2016/11/06/background-segmentation-removal-with-opencv)
- [OpenCV Documentation](https://docs.opencv.org/4.x/index.html)
