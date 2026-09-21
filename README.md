# Face Detection using Haar Cascades with OpenCV and Matplotlib

## Aim

To write a Python program using OpenCV to perform the following image manipulations:  
i) Extract ROI from an image.  
ii) Perform face detection using Haar Cascades in static images.  
iii) Perform eye detection in images.  
iv) Perform face detection with label in real-time video from webcam.

## Software Required

- Anaconda - Python 3.7 or above  
- OpenCV library (`opencv-python`)  
- Matplotlib library (`matplotlib`)  
- Jupyter Notebook or any Python IDE (e.g., VS Code, PyCharm)

## Algorithm

### I) Load and Display Images

- Step 1: Import necessary packages: `numpy`, `cv2`, `matplotlib.pyplot`  
- Step 2: Load grayscale images using `cv2.imread()` with flag `0`  
- Step 3: Display images using `plt.imshow()` with `cmap='gray'`

### II) Load Haar Cascade Classifiers

- Step 1: Load face and eye cascade XML files 
### III) Perform Face Detection in Images

- Step 1: Define a function `detect_face()` that copies the input image  
- Step 2: Use `face_cascade.detectMultiScale()` to detect faces  
- Step 3: Draw white rectangles around detected faces with thickness 10  
- Step 4: Return the processed image with rectangles  

### IV) Perform Eye Detection in Images

- Step 1: Define a function `detect_eyes()` that copies the input image  
- Step 2: Use `eye_cascade.detectMultiScale()` to detect eyes  
- Step 3: Draw white rectangles around detected eyes with thickness 10  
- Step 4: Return the processed image with rectangles  

### V) Display Detection Results on Images

- Step 1: Call `detect_face()` or `detect_eyes()` on loaded images  
- Step 2: Use `plt.imshow()` with `cmap='gray'` to display images with detected regions highlighted  

### VI) Perform Face Detection on Real-Time Webcam Video

- Step 1: Capture video from webcam using `cv2.VideoCapture(0)`  
- Step 2: Loop to continuously read frames from webcam  
- Step 3: Apply `detect_face()` function on each frame  
- Step 4: Display the video frame with rectangles around detected faces  
- Step 5: Exit loop and close windows when ESC key (key code 27) is pressed  
- Step 6: Release video capture and destroy all OpenCV windows  

## Program
### Developed by : VD Natchathira
### Reg no: 212224230178
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
image = cv2.imread("C:/Users/admin/Pictures/Screenshots/Screenshot 2026-09-07 150724.png")  # Replace with your image path
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
plt.imshow(image_rgb)
plt.title("Original Image")
plt.axis('on')
plt.show()
```
<img width="361" height="357" alt="image" src="https://github.com/user-attachments/assets/b72ccc47-c2ed-41cb-9c79-84a65b375eae" />

```
roi = image[100:420, 200:550]  # ROI coordinates (adjust as needed)
mask = np.zeros_like(image)
mask[100:420, 200:550] = roi
segmented_roi = cv2.bitwise_and(image, mask)
segmented_roi_rgb = cv2.cvtColor(segmented_roi, cv2.COLOR_BGR2RGB)
plt.imshow(segmented_roi_rgb)
plt.title("Segmented ROI")
plt.axis('off')
plt.show()
```
<img width="310" height="337" alt="Screenshot 2026-09-20 120346" src="https://github.com/user-attachments/assets/d1590b44-a646-42ce-99ff-07ab18e36722" />


```
import cv2
import numpy as np
import matplotlib.pyplot as plt
image = cv2.imread("C:/Users/admin/Pictures/Screenshots/Screenshot 2026-09-09 213358.png")  # Replace with your actual image file path
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)  # Convert BGR to RGB
plt.imshow(image_rgb)
plt.title("Original Image")
plt.axis('off')
```

<img width="466" height="207" alt="image" src="https://github.com/user-attachments/assets/ab12b4d2-2cb7-41ed-859f-dd1fdd19f61a" />

```
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
blurred_image = cv2.GaussianBlur(gray_image, (5, 5), 0)
edges = cv2.Canny(blurred_image, 50, 150)
plt.imshow(edges, cmap='gray')
plt.title("Canny Edge Detection")
plt.axis('off')
```
<img width="450" height="212" alt="image" src="https://github.com/user-attachments/assets/e4794d99-e729-4c2c-8b69-412613064c21" />

```
contours, _ = cv2.findContours(edges, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
result_image = image.copy()  
for contour in contours:
    if cv2.contourArea(contour) > 50:  
        x, y, w, h = cv2.boundingRect(contour)  
        cv2.rectangle(result_image, (x, y), (x + w, y + h), (0, 255, 0), 2)
plt.imshow(cv2.cvtColor(result_image, cv2.COLOR_BGR2RGB))
plt.title("Handwriting Detection")
plt.axis('off')
```
<img width="467" height="200" alt="image" src="https://github.com/user-attachments/assets/babb05ba-1e1c-47f4-820a-9e68b75c1aab" />

```
import cv2
import matplotlib.pyplot as plt

image_path = ("C:/Users/admin/Pictures/Screenshots/Screenshot 2026-09-20 115418.png")

image = cv2.imread(image_path)

if image is None:
    print("Image not found. Check the file path.")
else:
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
    print("Image loaded successfully")
lower = (40, 30, 40)
upper = (255, 255, 90)
mask = cv2.inRange(hsv, lower, upper)
contours, _ = cv2.findContours(
    mask,
    cv2.RETR_EXTERNAL,
    cv2.CHAIN_APPROX_SIMPLE
)
largest = max(contours, key=cv2.contourArea)

x, y, w, h = cv2.boundingRect(largest)
cv2.rectangle(
    image,
    (x, y),
    (x + w, y + h),
    (0, 255, 0),
    3
)
cv2.rectangle(
    image,
    (x, y),
    (x + w, y + h),
    (0, 255, 0),
    3
)

plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.axis("off")
plt.show()
```
<img width="418" height="215" alt="image" src="https://github.com/user-attachments/assets/7391978b-498e-4744-a026-c8756d25d5f1" />

## Result
Thus, the Python program using OpenCV was successfully implemented to extract ROI, detect faces and eyes using Haar Cascades in static images, and detect faces with labels in real-time webcam video.
