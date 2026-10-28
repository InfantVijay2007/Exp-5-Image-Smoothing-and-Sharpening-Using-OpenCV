# Exp-5--Record-Implementation-of-Filters

## Aim

To write a Python program using OpenCV to apply different smoothing filters (Averaging, Weighted Averaging, Gaussian, Median) and sharpening filters (Laplacian Kernel and Laplacian Operator) for image enhancement, and display each result separately along with the original image for comparison.

---

## The program performs the following operations:

- Read and display an input image  
- Apply Averaging filter  
- Apply Weighted Averaging filter  
- Apply Gaussian filter  
- Apply Median filter  
- Apply Laplacian sharpening using kernel  
- Apply Laplacian operator  
- Display all outputs for comparison  

---

##  Software Used

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (cv2)  
- NumPy  
- Matplotlib  

---

##  Algorithm

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:
Read the input image (e.g., `image.jpg`).

### Step 3:
Convert the image from BGR to RGB format for display.

### Step 4:
Apply Averaging Filter using `cv2.blur()`.

### Step 5:
Apply Weighted Averaging Filter using a custom kernel with `cv2.filter2D()`.

### Step 6:
Apply Gaussian Filter using `cv2.GaussianBlur()`.

### Step 7:
Apply Median Filter using `cv2.medianBlur()`.

### Step 8:
Apply Laplacian Sharpening using Kernel with `cv2.filter2D()`.

### Step 9:
Convert image to grayscale and apply Laplacian Operator using `cv2.Laplacian()`.

### Step 10:
Display all filtered images using a grid layout for comparison.

---

## Program

```py

import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read image
img = cv2.imread("taj.jpg")

if img is None:
    raise FileNotFoundError("Please check taj.jpg exists.")

rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# 1. Original
original = rgb.copy()

# 2. Averaging Filter
averaging = cv2.blur(rgb, (41, 41))

# 3. Weighted Averaging Filter
kernel = np.ones((21, 21), dtype=np.float32)
kernel[10, 10] = 500
kernel = kernel / kernel.sum()

weighted = cv2.filter2D(rgb, -1, kernel)

# 4. Gaussian Blur
gaussian = cv2.GaussianBlur(rgb, (51, 51), 0)

# 5. Median Blur
median = cv2.medianBlur(rgb, 21)

# 6. Laplacian Sharpening
blurred = cv2.GaussianBlur(rgb, (9, 9), 0)
sharpened = cv2.addWeighted(rgb, 3.0, blurred, -2.0, 0)

# 7. Grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# 8. Laplacian Edge Detection
lap = cv2.Laplacian(gray, cv2.CV_64F, ksize=3)
laplacian = cv2.convertScaleAbs(lap)
laplacian = cv2.threshold(
    laplacian, 35, 255, cv2.THRESH_BINARY
)[1]

# Display
images = [
    (original, "Original Image"),
    (averaging, "Strong Averaging Blur"),
    (weighted, "Weighted Averaging"),
    (gaussian, "Strong Gaussian Blur"),
    (median, "Median Blur"),
    (sharpened, "Strong Sharpening"),
    (gray, "Grayscale"),
    (laplacian, "Laplacian Edges")
]

plt.figure(figsize=(16, 10))

for i, (image, title) in enumerate(images):
    plt.subplot(2, 4, i + 1)

    if image.ndim == 2:
        plt.imshow(image, cmap="gray")
    else:
        plt.imshow(image)

    plt.title(title)
    plt.axis("off")

plt.tight_layout()
plt.show()




```

##  Developed By

- **Name:** INFANT VIJAY A
- **Register No:** 212225240052

---

##  Output


<img width="1267" height="558" alt="Screenshot 2026-10-28 221233" src="https://github.com/user-attachments/assets/a9bec673-e7e4-4915-a8e1-94a8164bcd31" />




### Smoothing Filters

- Averaging filter produces blurred image  
- Weighted averaging provides smoother result with less distortion  
- Gaussian filter preserves edges better while reducing noise  
- Median filter removes salt-and-pepper noise effectively  

###  Sharpening Filters

- Laplacian kernel enhances edges and fine details  
- Laplacian operator detects edges clearly in grayscale  

---

##  Result

Thus, smoothing filters and sharpening filters are successfully implemented using OpenCV.

The smoothing filters reduce noise and improve image quality, while sharpening filters enhance edges and details for better feature extraction.
