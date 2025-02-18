# Laplacian of Gaussian (LoG) Edge Detection (Manual Implementation)

## 📌 Overview
This project implements **Laplacian of Gaussian (LoG) Edge Detection** entirely from scratch using Python. The implementation does not use any built-in edge detection functions from libraries like OpenCV or SciPy. Instead, all operations—including convolution, Gaussian smoothing, and Laplacian filtering—are performed manually.

## 🔍 What is LoG?
Laplacian of Gaussian (LoG) is an edge detection method that combines two key steps:
1. **Gaussian Smoothing**: A Gaussian filter is applied to reduce noise in the image before edge detection.
2. **Laplacian Filtering**: A second-order derivative filter (Laplacian) is applied to highlight regions of rapid intensity change.

Edges are identified by detecting **zero-crossings** in the Laplacian-filtered image.

## ✨ Key Features
- **Fully manual implementation**: Convolution operations are performed using a custom function without built-in libraries.
- **Comparison of results**:
  - Laplacian applied to the original image.
  - Laplacian applied to the image after Gaussian smoothing (LoG).
- **Custom 3x3 kernels** for both Gaussian smoothing and Laplacian filtering.

## 🔧 Implementation Details
The process follows these steps:
1. **Load the Image**: OpenCV is used only to read the image.
2. **Manual Convolution**: A function applies a kernel to an image through element-wise multiplication and summation.
3. **Gaussian Smoothing**: A 3x3 Gaussian kernel is applied to smooth the image.
4. **Laplacian Filtering**: A 3x3 Laplacian kernel is applied to both the original and smoothed images.
5. **Comparison of Results**: The differences between direct Laplacian and LoG are visualized.

## 📜 Code Explanation
### **Manual Convolution Function:**
```python
import numpy as np

def manual_convolution(image, kernel):
    h, w = image.shape
    kh, kw = kernel.shape
    pad_h, pad_w = kh // 2, kw // 2
    padded_image = np.pad(image, ((pad_h, pad_w)), mode='constant', constant_values=0)
    convolved = np.zeros_like(image, dtype=np.float32)
    for i in range(h):
        for j in range(w):
            region = padded_image[i:i+kh, j:j+kw]
            convolved[i, j] = np.sum(region * kernel)
    return convolved
```

### **Kernels Used**
#### **Gaussian Kernel (3x3):**
```python
kernel_gaussian = np.array([
    [1, 2, 1],
    [2, 4, 2],
    [1, 2, 1]
]) / 16
```

#### **Laplacian Kernel (3x3):**
```python
kernel_laplacian = np.array([
    [0, -1, 0],
    [-1, 4, -1],
    [0, -1, 0]
])
```

## 🚀 Running the Project
### **1. Clone the repository:**
```sh
git clone <repository_url>
```
### **2. Install dependencies:**
```sh
pip install numpy opencv-python matplotlib
```
### **3. Run the script:**
```sh
python log_edge_detection.py
```

## 📊 Results
The output will display four images for comparison:
- 🖼 **Original Image**
- 🖼 **Gaussian Smoothed Image**
- 🖼 **Laplacian Applied to Original Image**
- 🖼 **Laplacian Applied After Gaussian Smoothing (LoG)**

This comparison helps visualize how smoothing affects edge detection.

## 🔮 Future Improvements
- Implement **adaptive thresholding** for better edge detection.
- Extend to **Canny Edge Detection** for further comparison.
- Optimize convolution using **NumPy vectorization**.

## 💁 Conclusion 
- Since Laplacian alone is sensitive to noise, Gaussian smoothening is used to remove noise first and then Laplacian is applied which makes it more effective than normal. 
