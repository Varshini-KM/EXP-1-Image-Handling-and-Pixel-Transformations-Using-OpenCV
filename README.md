# Image-Handling-and-Pixel-Transformations-Using-OpenCV

# AIM:
Write a Python program using OpenCV that performs the following tasks:

1. Read and Display an Image.
2. Adjust the brightness of an image.
3. Modify the image contrast.
4. Generate a third image using bitwise operations.

# Software Required:

* Anaconda - Python 3.7
* Jupyter Notebook (for interactive development and execution)

# Algorithm:
Step 1:
Load an image from your local directory and display it.

Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.
Display the original, brighter, and darker images.

Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).
Display the original, lower contrast, and higher contrast images.

Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

# Program Developed By:
Name: Yuuvasri R

Register Number: 212225230313

# Ex. No. 01

# Program:
Step1:
Load an image from your local directory and display it.
```python
import cv2
import matplotlib.pyplot as plt

# Read the image using OpenCV
img = cv2.imread('butterfly.jpg', cv2.IMREAD_COLOR)

# Convert BGR (OpenCV's default) to RGB (Matplotlib's expected color order)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# Display the image using Matplotlib
plt.imshow(img_rgb, cmap='viridis')  # You can change 'viridis' to another cmap or use None for RGB images
plt.title("Original Image")
plt.axis('off')  # Removes axis ticks and labels
plt.show()
```

Step2:
- Draw a line from the top-left to the bottom-right of the image.
- Draw a circle at the center of the image.
- Draw a rectangle around a specific region of interest in the image.
- Add the text "OpenCV Drawing" at the top-left corner of the image.
Draw a line from the top-left to the bottom-right of the image

```python
# Load the image
image = cv2.imread('butterfly.jpg') 

# Convert BGR (OpenCV's default) to RGB (Matplotlib's expected color order)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

img_rgb.shape

# Draw a line from top-left to bottom-right
line_img = cv2.line(img_rgb, (0, 0), (493, 356), (255, 0, 0), 2) # cv2.line(image, start_point, end_point, color, thickness)

plt.imshow(line_img, cmap='viridis')  
plt.title("Image with Line")
plt.axis('off')  
plt.show()
```

Draw a circle at the center of the image.

```python
# Load the image
image = cv2.imread('butterfly.jpg') 

# Convert BGR (OpenCV's default) to RGB (Matplotlib's expected color order)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

img_rgb.shape

circle_img = cv2.circle(img_rgb,(246,178),100,(255,0,0),10) # cv2.circle(image, center, radius, color, thickness)

plt.imshow(circle_img, cmap='viridis')  
plt.title("Image with Circle")
plt.axis('off')  
plt.show()
```

Draw a rectangle around  the whole image

```python
# Load the image
image = cv2.imread('butterfly.jpg') 

# Convert BGR (OpenCV's default) to RGB (Matplotlib's expected color order)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

img.shape

# Draw a rectangle around the Whole image
rectangle_img = cv2.rectangle(img_rgb, (0, 0), (493, 356), (0, 0, 255), 10)  # cv2.rectangle(image, start_point, end_point, color, thickness)

plt.imshow(rectangle_img, cmap='viridis')  
plt.title("Image with Rectangle")
plt.axis('off')  
plt.show()
```

Add the text "OpenCV Drawing" at the top-left corner of the image.

```python
# Load the image
image = cv2.imread('butterfly.jpg') 

# Convert BGR (OpenCV's default) to RGB (Matplotlib's expected color order)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# Add text to the image
text_img = cv2.putText(img_rgb, "OpenCV Drawing", (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1, (255, 255, 255), 10)  ## cv2.putText(image, text, position, font, font_scale, color, thickness)

plt.imshow(text_img, cmap='viridis')  
plt.title("Image with Text")
plt.axis('off')  
plt.show()
```

Step3:
- Convert the image from RGB to HSV and display it.
- Convert the image from RGB to GRAY and display it.
- Convert the image from RGB to YCrCb and display it.
- Convert the HSV image back to RGB and display it.
```python
# Load the image
image = cv2.imread('butterfly.jpg') 

image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Original RGB Image
plt.imshow(image_rgb)
plt.title("Original RGB Image")
plt.axis("off")

# Convert RGB to HSV
image_hsv = cv2.cvtColor(image_rgb, cv2.COLOR_RGB2HSV)

# HSV Image
plt.imshow(image_hsv)
plt.title("HSV Image")
plt.axis("off")

# Convert RGB to GRAY
image_gray = cv2.cvtColor(image_rgb, cv2.COLOR_RGB2GRAY)

# Grayscale Image
plt.imshow(image_gray, cmap='gray')
plt.title("Grayscale Image")
plt.axis("off")

# Convert RGB to YCrCb
image_ycrcb = cv2.cvtColor(image_rgb, cv2.COLOR_RGB2YCrCb)

# YCrCb Image
plt.imshow(image_ycrcb)
plt.title("YCrCb Image")
plt.axis("off")

# Convert HSV back to RGB
image_hsv_to_rgb = cv2.cvtColor(image_hsv, cv2.COLOR_HSV2RGB)

plt.imshow(image_hsv_to_rgb)
plt.title("HSV to RGB Image")
plt.axis("off")
```

Step4:
- Access and print the value of the pixel at coordinates (100, 100).
- Modify the color of the pixel at (200, 200) to white.
```python
# Modify a block of pixels (150x150) to white, starting from (200, 200)
image[200:350, 200:350] = [255, 255, 255]  # Rows: 200-349, Columns: 200-349

# Convert BGR to RGB for displaying with Matplotlib
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Display the modified image
plt.imshow(image_rgb)
plt.title("Image with 150x150 White Block")
plt.axis("off")
plt.show()
```

Step5:
- Resize the original image to half its size and display it.
```python
# Load the image
image = cv2.imread('butterfly.jpg') 

image.shape

# Resize the image to half its size
resized_image = cv2.resize(image, (493 // 2, 356 // 2))  # (new_width, new_height)

# Convert BGR to RGB for displaying with Matplotlib
resized_image_rgb = cv2.cvtColor(resized_image, cv2.COLOR_BGR2RGB)

resized_image_rgb.shape

# Display the resized image
plt.imshow(resized_image_rgb)
plt.title("Resized Image (Half Size)")
plt.axis("off")
plt.show()
```

Step6:
- Crop a region of interest (ROI) from the image (e.g., a 100x100 pixel area starting at (50, 50)) and display it.
```python
# Load the image
image = cv2.imread('butterfly.jpg') 

image.shape

# Crop a 300x300 region starting from (50, 50)
roi = image[50:350, 50:350]  # Rows: 50-349, Columns: 50-349

# Convert BGR to RGB for displaying with Matplotlib
roi_rgb = cv2.cvtColor(roi, cv2.COLOR_BGR2RGB)

# Display the cropped region (ROI)
plt.imshow(roi_rgb)
plt.title("Cropped Region of Interest (ROI)")
plt.axis("off")
plt.show()
```

Step7:
- Flip the original image horizontally and display it.
- Flip the original image vertically and display it.
```python
# Load the image
image = cv2.imread('butterfly.jpg') 

# Flip the image horizontally (left-right)
flipped_horizontally = cv2.flip(image, 1)

# Convert BGR to RGB for displaying with Matplotlib
flipped_horizontally_rgb = cv2.cvtColor(flipped_horizontally, cv2.COLOR_BGR2RGB)

# Horizontal flip
plt.imshow(flipped_horizontally_rgb)
plt.title("Flipped Horizontally")
plt.axis("off")

# Flip the image vertically (up-down)
flipped_vertically = cv2.flip(image, 0)

# Convert BGR to RGB for displaying with Matplotlib
flipped_vertically_rgb = cv2.cvtColor(flipped_vertically, cv2.COLOR_BGR2RGB)

# Vertical flip
plt.imshow(flipped_vertically_rgb)
plt.title("Flipped Vertically")
plt.axis("off")
```

Step8:
- Save the final modified image to your local directory.
```python
# Save the final modified image to your local directory
cv2.imwrite('final.jpg', flipped_vertically)
```

# Output:
<img width="561" height="442" alt="image" src="https://github.com/user-attachments/assets/b3dcf196-a94f-430e-8e2a-d439ee73bda4" />
<img width="562" height="437" alt="image" src="https://github.com/user-attachments/assets/c542d33a-998d-4a36-85d9-3a90a43c2e7f" />
<img width="562" height="446" alt="image" src="https://github.com/user-attachments/assets/f3b3a922-8c81-4ed5-a68b-4843e06c2275" />
<img width="559" height="440" alt="image" src="https://github.com/user-attachments/assets/318656f4-bdc7-44bd-b461-6a918ded3198" />
<img width="564" height="428" alt="image" src="https://github.com/user-attachments/assets/46f1fecf-e93c-4f99-aa30-76420f7a85fc" />
<img width="577" height="436" alt="image" src="https://github.com/user-attachments/assets/4287a6ee-61e4-4246-88c7-8ee16d739aaf" />
<img width="556" height="433" alt="image" src="https://github.com/user-attachments/assets/1bd46afc-284c-444b-89b2-680be413008c" />
<img width="564" height="442" alt="image" src="https://github.com/user-attachments/assets/4e27b6fb-99ab-4d50-848a-5096c0b5b1c4" />
<img width="559" height="437" alt="image" src="https://github.com/user-attachments/assets/7f0a6057-d998-4769-853a-1f486206e4a0" />
<img width="559" height="439" alt="image" src="https://github.com/user-attachments/assets/e955ec24-eff3-4039-8b1c-7394c3b13eff" />
<img width="570" height="458" alt="image" src="https://github.com/user-attachments/assets/e1877135-1709-4d8f-8b59-a39f27b23a7b" />
<img width="566" height="455" alt="image" src="https://github.com/user-attachments/assets/48c23988-f123-42bf-b67c-41dc03c76b58" />
<img width="418" height="458" alt="image" src="https://github.com/user-attachments/assets/c71342e0-aa65-456e-8a8e-9e2d4a708437" />
<img width="560" height="436" alt="image" src="https://github.com/user-attachments/assets/fd3d5446-40bd-442a-9b66-b52441ece363" />
<img width="561" height="437" alt="image" src="https://github.com/user-attachments/assets/5fdb4152-ae20-474a-83b3-506aa6740609" />






# Result:
Thus, the image was read, displayed, processed and saved successfully using OpenCV in Python.
