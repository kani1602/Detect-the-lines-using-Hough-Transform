# Detect-the-lines-using-Hough-Transform
# Lane Detection
# AIM:
To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.
# Learning Objective:
1.Understand each stage of image processing

2.Learn how to build a complete computer vision pipeline

3.Practice writing code in guided sections

# Software Used
Anaconda – Python 3.7

Jupyter Notebook / VS Code

OpenCV (cv2)

NumPy

Matplotlib

# Algorithm & Explanation
# Step 1: Import Libraries
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
# Step 2: Read the Image
```
img = cv2.imread("lan.jpg")

if img is None:
    print("Error: Image not found. Check the image path.")
else:
    print("Image loaded successfully")
```
# Step 3: Convert to Grayscale
```
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")
plt.show()
```
# Step 4: Display Images
```
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.show()
```
# Step 5: Thresholding
```
ret, threshold = cv2.threshold(
    gray,
    127,
    255,
    cv2.THRESH_BINARY
)

plt.imshow(threshold, cmap="gray")
plt.title("Thresholded Image")
plt.axis("off")
plt.show()
```
# Step 6: Region of Interest (ROI)
```
height, width = gray.shape

mask = np.zeros_like(gray)

polygon = np.array([[
    (0, height),
    (width, height),
    (int(width * 0.6), int(height * 0.55)),
    (int(width * 0.4), int(height * 0.55))
]], dtype=np.int32)

cv2.fillPoly(mask, polygon, 255)

roi = cv2.bitwise_and(threshold, mask)

plt.imshow(roi, cmap="gray")
plt.title("Region of Interest")
plt.axis("off")
plt.show()
```
# Step 7: Edge Detection (Canny)
```
edges = cv2.Canny(roi, 50, 150)

plt.imshow(edges, cmap="gray")
plt.title("Canny Edge Detection")
plt.axis("off")
plt.show()
```
# Step 8: Gaussian Blur
```
blur = cv2.GaussianBlur(
    edges,
    (5, 5),
    0
)

plt.imshow(blur, cmap="gray")
plt.title("Gaussian Blur")
plt.axis("off")
plt.show()
```
# Step 9: Hough Transform
```
lines = cv2.HoughLinesP(
    blur,
    1,
    np.pi / 180,
    threshold=50,
    minLineLength=50,
    maxLineGap=100
)

print("Detected Lines:", lines)
```
# Step 10: Lane Detection Logic
```
lane = cv2.cvtColor(
    img,
    cv2.COLOR_BGR2RGB
).copy()

if lines is not None:

    for line in lines:

        line = np.array(line).reshape(-1)

        if len(line) == 4:

            x1, y1, x2, y2 = line

            cv2.line(
                lane,
                (int(x1), int(y1)),
                (int(x2), int(y2)),
                (255, 0, 0),
                5
            )

plt.figure(figsize=(10, 6))
plt.imshow(lane)
plt.title("Final Lane Detection")
plt.axis("off")
plt.show()
```
# Output:
# original image:

<img width="245" height="258" alt="image" src="https://github.com/user-attachments/assets/0bcd1408-1a41-4e02-9169-33619409d990" />


# Grayscale image:

<img width="245" height="258" alt="image" src="https://github.com/user-attachments/assets/8a0b241d-e85d-4abd-9a5c-cd5518b12cd7" />


# Thresholded image:

<img width="245" height="258" alt="image" src="https://github.com/user-attachments/assets/848ff724-a39e-4479-bb80-995287f99a8a" />

# ROI image:
<img width="245" height="258" alt="image" src="https://github.com/user-attachments/assets/508b5400-5417-4b4b-a0dc-366a68022a73" />


# Edge detected image:
<img width="404" height="410" alt="image" src="https://github.com/user-attachments/assets/e8c30c21-d958-4c88-94a3-3c45a8273932" />

# Gaussian blur:
<img width="404" height="410" alt="image" src="https://github.com/user-attachments/assets/07caded8-97b6-422f-a061-7e3c06da078c" />


# Final lane detection:
<img width="500" height="503" alt="image" src="https://github.com/user-attachments/assets/d97168f7-ce30-4947-a2ee-f1d4f9af043f" />


# Result:
Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.
