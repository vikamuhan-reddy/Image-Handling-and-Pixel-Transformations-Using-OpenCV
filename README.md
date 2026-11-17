# Image Handling and Pixel Transformations Using OpenCV

## AIM

Write a Python program using OpenCV to: 1. Read and display an image. 2.
Adjust the brightness of an image. 3. Modify the image contrast. 4.
Generate a third image using bitwise operations.

## Software Required

-   Anaconda -- Python 3.7
-   Jupyter Notebook

## Algorithm

1.  Load an image from the local directory and display it.
2.  Create a matrix of ones (`float64`) to adjust brightness.
3.  Add and subtract a constant matrix to create brighter and darker
    images.
4.  Create higher-contrast images using scaling factors of 1.1 and 1.2,
    and a lower-contrast image using 0.8.
5.  Split `Boy.jpg` into B, G, R channels and display them.
6.  Convert the image to HSV, split H, S, V channels, and display them.
7.  Apply a bitwise operation using a mask to generate another image.

## Program Developed By

-   **Name:** \[Your Name Here\]
-   **Register Number:** \[Your Register Number Here\]

# Ex. No. 01

> **Note:** Keep `Eagle_in_Flight.jpg`, `Apollo-11-launch.jpg`, and
> `Boy.jpg` in the same folder as your Jupyter Notebook. Adjust crop and
> rectangle coordinates to match your actual images.

## 1. Read the image (`Eagle_in_Flight.jpg`) as a grayscale image

``` python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img_gray = cv2.imread('Eagle_in_Flight.jpg', cv2.IMREAD_GRAYSCALE)
```

## 2. Print the image width, height and channel

``` python
height, width = img_gray.shape

print("Width:", width)
print("Height:", height)
print("Channel: 1 (Grayscale)")
```

## 3. Display the image using `matplotlib imshow()`

``` python
plt.imshow(img_gray, cmap='gray')
plt.title('Eagle - Grayscale')
plt.axis('off')
plt.show()
```

## 4. Save the image as a PNG file using `cv2.imwrite()`

``` python
cv2.imwrite('Eagle.png', img_gray)
```

## 5. Read the saved image as a colour image using `cv2.cvtColor()`

``` python
img_color = cv2.cvtColor(img_gray, cv2.COLOR_GRAY2BGR)
```

## 6. Display the colour image and print width, height and channel

``` python
height, width, channel = img_color.shape

print("Width:", width)
print("Height:", height)
print("Channel:", channel)

plt.imshow(cv2.cvtColor(img_color, cv2.COLOR_BGR2RGB))
plt.title('Eagle - Colour')
plt.axis('off')
plt.show()
```

## 7. Crop the image to extract the eagle alone

``` python
# Format: image[y1:y2, x1:x2]
cropped = img_color[50:300, 100:400]

plt.imshow(cv2.cvtColor(cropped, cv2.COLOR_BGR2RGB))
plt.title('Cropped Eagle')
plt.axis('off')
plt.show()
```

## 8. Resize the cropped image by a factor of 2x

``` python
resized = cv2.resize(cropped, None, fx=2, fy=2)

plt.imshow(cv2.cvtColor(resized, cv2.COLOR_BGR2RGB))
plt.title('Resized Eagle')
plt.axis('off')
plt.show()
```

## 9. Flip the resized image horizontally

``` python
flipped = cv2.flip(resized, 1)

plt.imshow(cv2.cvtColor(flipped, cv2.COLOR_BGR2RGB))
plt.title('Horizontally Flipped Eagle')
plt.axis('off')
plt.show()
```

## 10. Read the image (`Apollo-11-launch.jpg`)

``` python
apollo = cv2.imread('Apollo-11-launch.jpg')

plt.imshow(cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB))
plt.title('Apollo 11 Launch')
plt.axis('off')
plt.show()
```

## 11. Add text to the dark area at the bottom of the image

``` python
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN

height, width = apollo.shape[:2]
font_scale = 1.5
thickness = 2
text_size = cv2.getTextSize(text, font_face, font_scale, thickness)[0]
x = (width - text_size[0]) // 2
y = height - 20

cv2.putText(apollo, text, (x, y), font_face, font_scale,
            (255, 255, 255), thickness)
```

## 12. Draw a magenta rectangle around the launch tower and rocket

``` python
rect_color = (255, 0, 255)  # Magenta in BGR format

# Change these coordinates to fit the rocket and launch tower
cv2.rectangle(apollo, (200, 50), (600, 500), rect_color, 3)
```

## 13. Display the final annotated image

``` python
plt.imshow(cv2.cvtColor(apollo, cv2.COLOR_BGR2RGB))
plt.title('Annotated Apollo 11 Launch')
plt.axis('off')
plt.show()
```

## 14. Read the image (`Boy.jpg`)

``` python
img = cv2.imread('Boy.jpg')

plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Boy Image')
plt.axis('off')
plt.show()
```

## 15. Adjust the brightness of the image

``` python
matrix_ones = np.ones(img.shape, dtype=np.float64)
```

## 16. Create brighter and darker images

``` python
matrix = matrix_ones * 50

img_brighter = cv2.add(img, matrix)
img_darker = cv2.subtract(img, matrix)
```

## 17. Display the original, darker and brighter images

``` python
plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB))
plt.title('Darker Image')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB))
plt.title('Brighter Image')
plt.axis('off')

plt.tight_layout()
plt.show()
```

## 18. Modify the image contrast

``` python
matrix1 = np.ones(img.shape, dtype=np.float64) * 1.1
matrix2 = np.ones(img.shape, dtype=np.float64) * 1.2

img_higher1 = cv2.multiply(img, matrix1)
img_higher2 = cv2.multiply(img, matrix2)
img_lower = cv2.multiply(img, 0.8)
```

## 19. Display the original, lower-contrast and higher-contrast images

``` python
plt.figure(figsize=(16, 4))

plt.subplot(1, 4, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original')
plt.axis('off')

plt.subplot(1, 4, 2)
plt.imshow(cv2.cvtColor(img_lower, cv2.COLOR_BGR2RGB))
plt.title('Lower Contrast')
plt.axis('off')

plt.subplot(1, 4, 3)
plt.imshow(cv2.cvtColor(img_higher1, cv2.COLOR_BGR2RGB))
plt.title('Contrast 1.1')
plt.axis('off')

plt.subplot(1, 4, 4)
plt.imshow(cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB))
plt.title('Contrast 1.2')
plt.axis('off')

plt.tight_layout()
plt.show()
```

## 20. Split the image into B, G, R components and display the channels

``` python
b, g, r = cv2.split(img)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(b, cmap='gray')
plt.title('Blue Channel')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(g, cmap='gray')
plt.title('Green Channel')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(r, cmap='gray')
plt.title('Red Channel')
plt.axis('off')

plt.tight_layout()
plt.show()
```

## 21. Merge the B, G, R channels and display with the original image

``` python
merged = cv2.merge([b, g, r])

plt.figure(figsize=(8, 4))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(merged, cv2.COLOR_BGR2RGB))
plt.title('Merged BGR Image')
plt.axis('off')

plt.tight_layout()
plt.show()
```

## 22. Split the image into H, S, V components and display the channels

``` python
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(hsv)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(h, cmap='gray')
plt.title('Hue')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(s, cmap='gray')
plt.title('Saturation')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(v, cmap='gray')
plt.title('Value')
plt.axis('off')

plt.tight_layout()
plt.show()
```

## 23. Merge the H, S, V channels and display with the original image

``` python
merged_hsv = cv2.merge([h, s, v])
merged_bgr = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)

plt.figure(figsize=(8, 4))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB))
plt.title('Merged HSV Image')
plt.axis('off')

plt.tight_layout()
plt.show()
```

## 24. Generate a third image using bitwise operations

``` python
# Create a white rectangular mask
mask = np.zeros(img.shape[:2], dtype=np.uint8)
cv2.rectangle(mask, (50, 50), (300, 300), 255, -1)

# Apply bitwise AND operation
bitwise_img = cv2.bitwise_and(img, img, mask=mask)

plt.figure(figsize=(8, 4))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(bitwise_img, cv2.COLOR_BGR2RGB))
plt.title('Bitwise AND Image')
plt.axis('off')

plt.tight_layout()
plt.show()
```

## Output
### i) Read and Display an Image
<img width="667" height="510" alt="image" src="https://github.com/user-attachments/assets/77e8f355-50fa-4ab3-b9d1-28bdc2bc3900" />
<img width="652" height="408" alt="image" src="https://github.com/user-attachments/assets/6f539faa-27e7-407f-9d4c-e5b5d9f48232" />
<img width="690" height="508" alt="image" src="https://github.com/user-attachments/assets/b3c34392-1225-4b12-b1fc-cd0d52c70ed4" />

### ii) Adjust Image Brightness
<img width="1292" height="342" alt="image" src="https://github.com/user-attachments/assets/a8435e7f-616e-481e-a1e3-ebfd9c866e05" />

### iii) Modify Image Contrast
<img width="1253" height="262" alt="image" src="https://github.com/user-attachments/assets/f45956a6-8f49-4988-8532-1ba32dd9bf78" />

### iv) Bitwise Operations
<img width="706" height="502" alt="image" src="https://github.com/user-attachments/assets/ece7cc13-4c1a-4743-9b57-2e876dc7de4e" />


## Result

Thus, images were successfully read, displayed, cropped, resized,
flipped and annotated. Brightness and contrast adjustments,
colour-channel splitting and merging, and bitwise operations were
performed using Python and OpenCV.
