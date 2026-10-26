# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (palace.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** [Your Name Here]  
- **Register Number:** [Your Register Number Here]

  ### Ex. No. 01

#### 1. Read the image ('butterfly.jpg') using OpenCV imread() as a grayscale image.
```python
img = cv2.imread('butterfly.jpg', cv2.IMREAD_GRAYSCALE)
```

#### 2. Print the image width, height & Channel.
```python
h, w = img.shape[:2]
c = 1 if img.ndim == 2 else img.shape[2]
print('Width:', w, ' Height:', h, ' Channels:', c)
```

#### 3. Display the image using matplotlib imshow().
```python
plt.imshow(img, cmap='gray')
plt.title('Grayscale Butterfly')
plt.axis('off')
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
cv2.imwrite('butterfly.png', img)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
saved = cv2.imread('butterfly.png')                 # loads as 3-channel BGR
color = cv2.cvtColor(saved, cv2.COLOR_BGR2RGB)   # BGR -> RGB for matplotlib
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
plt.imshow(color)
plt.title('Colour Image (RGB)')
plt.axis('off')
plt.show()
h, w, c = color.shape
print('Width:', w, ' Height:', h, ' Channels:', c)
```

#### 7. Crop the image to extract any specific (Butterfly alone) object from the image.
```python
# the saved PNG is grayscale, so take the crop from the original colour file
orig = cv2.cvtColor(cv2.imread('butterfly.jpg'), cv2.COLOR_BGR2RGB)

# Crop the butterfly alone: rows (y) 15-315, columns (x) 5-485
crop = orig[15:315, 5:485]
plt.imshow(crop)
plt.title('Cropped Butterfly')
plt.axis('off')
plt.show()
```

#### 8. Resize the image up by a factor of 2x.
```python
big = cv2.resize(crop, None, fx=2, fy=2, interpolation=cv2.INTER_CUBIC)
plt.imshow(big)
plt.title('Resized 2x')
plt.axis('off')
plt.show()
print('New size (H, W):', big.shape[:2])
```

#### 9. Flip the cropped/resized image horizontally. (Butterfly image)
```python
flip = cv2.flip(big, 1)   # 1 = horizontal flip
plt.imshow(flip)
plt.title('Flipped Horizontally')
plt.axis('off')
plt.show()
```

#### 10. Read in the image ('starry.jpg').
```python
art = cv2.imread('starry.jpg', cv2.IMREAD_COLOR)
art = cv2.cvtColor(art, cv2.COLOR_BGR2RGB)
plt.imshow(art)
plt.title('Starry Night')
plt.axis('off')
plt.show()
```

#### 11. Add the following text to the bottom of the image (centered on the image):
```python
text = 'The Starry Night, Van Gogh, 1889'
font_face = cv2.FONT_HERSHEY_PLAIN
scale = 1.6
thick = 2
note = art.copy()
H, W = note.shape[:2]

# Measure the text so it can be centred
(tw, th), base = cv2.getTextSize(text, font_face, scale, thick)
x = (W - tw) // 2          # horizontally centred
y = H - 18                 # near the bottom
cv2.putText(note, text, (x, y), font_face, scale, (255, 255, 255), thick, cv2.LINE_AA)
```

#### 12. Draw a magenta rectangle that encompasses the tall dark tree.
```python
rect_color = (255, 0, 255)   # magenta
# top-left (x, y) and bottom-right (x, y) enclosing the tall dark tree
cv2.rectangle(note, (100, 45), (360, 595), rect_color, 3)
```

#### 13. Display the final annotated image.
```python
plt.figure(figsize=(10, 8))
plt.imshow(note)
plt.title('Final Annotated Image')
plt.axis('off')
plt.show()
```

#### 14. Read the image ('palace.jpg').
```python
palace = cv2.imread('palace.jpg')
```

#### 15. Adjust the brightness of the image.
```python
# Create a matrix of ones (with data type float64)
ones = np.ones(palace.shape, dtype='float64') * 50   # brightness offset = 50
matrix = ones.astype('uint8')                        # same dtype as the image
```

#### 16. Create brighter and darker images.
```python
bright = cv2.add(palace, matrix)
dark = cv2.subtract(palace, matrix)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
plt.figure(figsize=(15, 4))
for i, (im, t) in enumerate([(palace, 'Original Image'), (dark, 'Darker Image'), (bright, 'Brighter Image')]):
    plt.subplot(1, 3, i + 1)
    plt.imshow(cv2.cvtColor(im, cv2.COLOR_BGR2RGB))
    plt.title(t)
    plt.axis('off')
plt.show()
```

#### 18. Modify the image contrast.
```python
# Higher contrast using scale factors 1.1 and 1.2 (without overflow fix)
matrix1 = np.ones(palace.shape, dtype='float64') * 1.1
matrix2 = np.ones(palace.shape, dtype='float64') * 1.2
high1 = np.uint8(np.multiply(palace.astype('float64'), matrix1))
high2 = np.uint8(np.multiply(palace.astype('float64'), matrix2))

# Lower contrast (scale below 1) for comparison
matrix0 = np.ones(palace.shape, dtype='float64') * 0.8
low = np.uint8(np.multiply(palace.astype('float64'), matrix0))
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
plt.figure(figsize=(18, 4))
for i, (im, t) in enumerate([(palace, 'Original'), (low, 'Lower Contrast'), (high1, 'Higher Contrast 1.1'), (high2, 'Higher Contrast 1.2')]):
    plt.subplot(1, 4, i + 1)
    plt.imshow(cv2.cvtColor(im, cv2.COLOR_BGR2RGB))
    plt.title(t)
    plt.axis('off')
plt.show()
```

#### 20. Split the image (palace.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(palace)
plt.figure(figsize=(15, 4))
for i, (ch, t) in enumerate([(b, 'Blue'), (g, 'Green'), (r, 'Red')]):
    plt.subplot(1, 3, i + 1)
    plt.imshow(ch, cmap='gray')
    plt.title(t + ' channel')
    plt.axis('off')
plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged = cv2.merge((b, g, r))
plt.figure(figsize=(10, 4))
plt.subplot(1, 2, 1); plt.imshow(cv2.cvtColor(palace, cv2.COLOR_BGR2RGB)); plt.title('Original'); plt.axis('off')
plt.subplot(1, 2, 2); plt.imshow(cv2.cvtColor(merged, cv2.COLOR_BGR2RGB)); plt.title('Merged (B, G, R)'); plt.axis('off')
plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv = cv2.cvtColor(palace, cv2.COLOR_BGR2HSV)
hue, sat, val = cv2.split(hsv)
plt.figure(figsize=(15, 4))
for i, (ch, t) in enumerate([(hue, 'Hue'), (sat, 'Saturation'), (val, 'Value')]):
    plt.subplot(1, 3, i + 1)
    plt.imshow(ch, cmap='gray')
    plt.title(t + ' channel')
    plt.axis('off')
plt.show()
```

#### 23. Merged the H, S, V, displays along with original image.
```python
mergedhsv = cv2.merge((hue, sat, val))
back = cv2.cvtColor(mergedhsv, cv2.COLOR_HSV2RGB)   # back to RGB so colours display correctly
plt.figure(figsize=(10, 4))
plt.subplot(1, 2, 1); plt.imshow(cv2.cvtColor(palace, cv2.COLOR_BGR2RGB)); plt.title('Original'); plt.axis('off')
plt.subplot(1, 2, 2); plt.imshow(back); plt.title('Merged (H, S, V)'); plt.axis('off')
plt.show()
```

## Output:
- **i)** Read and Display an Image.  




- **ii)** Adjust Image Brightness.  




- **iii)** Modify Image Contrast.  




- **iv)** Generate Third Image Using Bitwise Operations.  




## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.
