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
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** T.K. GEETHU NEEPA
- **Register Number:** 212225220033

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
img =cv2.imread('Eagle_in_Flight.jpg',cv2.IMREAD_COLOR)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

#### 2. Print the image width, height & Channel.
```python
img.shape
```

#### 3. Display the image using matplotlib imshow().
```python
img_gray = cv2.cvtColor(img_rgb, cv2.COLOR_RGB2GRAY)
plt.imshow(img_gray,cmap='gray')
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
img=cv2.imread('Eagle_in_Flight.jpg')
cv2.imwrite('Eagle.png',img)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
img=cv2.imread('Eagle.png')
img_rgb = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
plt.imshow(img)
plt.show()
img.shape
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
crop = img_rgb[0:450,200:550] 
plt.imshow(crop[:,:,::-1])
plt.title("Cropped Region")
plt.axis("off")
plt.show()
crop.shape
```

#### 8. Resize the image up by a factor of 2x.
```python
res= cv2.resize(crop,(200*2, 200*2))
```

#### 9. Flip the cropped/resized image horizontally.
```python
flip= cv2.flip(res,1)
plt.imshow(flip[:,:,::-1])
plt.title("Flipped Horizontally")
plt.axis("off")
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
img=cv2.imread('Apollo-11-launch.jpg',cv2.IMREAD_COLOR)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
img_rgb.shape
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
text = cv2.putText(img_rgb, "Apollo 11 Saturn V Launch, July 16, 1969", (300, 700),cv2.FONT_HERSHEY_SIMPLEX, 1, (255, 255, 255), 2)  
plt.imshow(text, cmap='gray')  
plt.title("New image")
plt.show()  
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
rcol= (255, 0, 255)
cv2.rectangle(img_rgb, (400, 100), (800, 650), rcol, 3)  
```

#### 13. Display the final annotated image.
```python
plt.title("Annotated image")
plt.imshow(img_rgb)
plt.show()
```

#### 14. Read the image ('Boy.jpg').
```python
img =cv2.imread('boy.jpg',cv2.IMREAD_COLOR)
img_rgb= cv2.cvtColor(img, cv2.COLOR_BGR2RGB) 
```

#### 15. Adjust the brightness of the image.
```python
m = np.ones(img_rgb.shape, dtype="uint8") * 50
```

#### 16. Create brighter and darker images.
```python
img_brighter = cv2.add(img_rgb, m)  
img_darker = cv2.subtract(img_rgb, m)  
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(img_rgb), plt.title("Original Image"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(img_brighter), plt.title("Brighter Image"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(img_darker), plt.title("Darker Image"), plt.axis("off")
plt.show()
```

#### 18. Modify the image contrast.
```python
matrix1 = np.ones(img_rgb.shape, dtype="float32") * 1.1
matrix2 = np.ones(img_rgb.shape, dtype="float32") * 1.2
img_higher1 = cv2.multiply(img.astype("float32"), matrix1).clip(0,255).astype("uint8")
img_higher2 = cv2.multiply(img.astype("float32"), matrix2).clip(0,255).astype("uint8")
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(img), plt.title("Original Image"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(img_higher1), plt.title("Higher Contrast (1.1x)"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(img_higher2), plt.title("Higher Contrast (1.2x)"), plt.axis("off")
plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(img)
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(b, cmap='gray'), plt.title("Blue Channel"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(g, cmap='gray'), plt.title("Green Channel"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(r, cmap='gray'), plt.title("Red Channel"), plt.axis("off")
plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged_rgb = cv2.merge([r, g, b])
plt.figure(figsize=(5,5))
plt.imshow(merged_rgb)
plt.title("Merged RGB Image")
plt.axis("off")
plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv_img = cv2.cvtColor(img, cv2.COLOR_RGB2HSV)
h, s, v = cv2.split(hsv_img)
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(h, cmap='gray'), plt.title("Hue Channel"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(s, cmap='gray'), plt.title("Saturation Channel"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(v, cmap='gray'), plt.title("Value Channel"), plt.axis("off")
plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.

```pythonmerged_hsv = cv2.cvtColor(cv2.merge([h, s, v]), cv2.COLOR_HSV2RGB)
combined = np.concatenate((img_rgb, merged_hsv), axis=1)
plt.figure(figsize=(10, 5))
plt.imshow(combined)
plt.title("Original Image  &  Merged HSV Image")
plt.axis("off")
plt.show()# YOUR CODE HERE
```

## Output:
- **i)** Read and Display an Image.
-   1.Read 'Eagle_in_Flight.jpg' as grayscale and display:
-   <img width="682" height="527" alt="Screenshot 2026-07-28 111652" src="https://github.com/user-attachments/assets/4939a8d9-3157-487e-8f77-6be71ced827b" />
2.Save image as PNG and display:

<img width="702" height="532" alt="image" src="https://github.com/user-attachments/assets/69980d8c-9793-41a1-9139-56cd79f86393" />
3.Cropped image:

<img width="392" height="517" alt="image" src="https://github.com/user-attachments/assets/141f2d49-d829-49a8-b805-e919a7b15bf2" />
4.Resize and flip Horizontally:

<img width="476" height="507" alt="image" src="https://github.com/user-attachments/assets/ebdb146f-04a4-46e9-b7b6-234faf1de50e" />
5.Read 'Apollo-11-launch.jpg' and Display the final annotated image:

<img width="700" height="411" alt="image" src="https://github.com/user-attachments/assets/d4d573f4-963b-45b3-b347-286bd16b53b4" />

- **ii)** Adjust Image Brightness.
- 1.Create brighter and darker images and display:

- <img width="352" height="280" alt="image" src="https://github.com/user-attachments/assets/df20eee9-b020-4b40-8192-3b8c97746995" />

<img width="362" height="277" alt="image" src="https://github.com/user-attachments/assets/4d043389-88e4-43e9-a9a9-125bb2a6f50a" />

<img width="362" height="312" alt="image" src="https://github.com/user-attachments/assets/93a0191b-37bf-4c07-a604-48ead83c4862" />


 
- **iii)** Modify Image Contrast.
-1. Modify contrast using scaling factors 1.1 and 1.2:

 <img width="337" height="287" alt="image" src="https://github.com/user-attachments/assets/77921d6b-b6c2-4fa8-98f2-5084417988ec" />

 <img width="352" height="306" alt="image" src="https://github.com/user-attachments/assets/60310dd3-a044-467b-89a7-b5f47edd99ea" />

 <img width="366" height="297" alt="image" src="https://github.com/user-attachments/assets/772e6db8-f0b0-4fa5-a106-faae16fdb6a1" />



- **iv)** Generate Third Image Using Bitwise Operations.
- 1.Split 'Boy.jpg' into B, G, R components and display:

- <img width="377" height="297" alt="image" src="https://github.com/user-attachments/assets/76abe28c-45ab-4389-ac41-8653351813b1" />

<img width="360" height="297" alt="image" src="https://github.com/user-attachments/assets/e7a2b2a7-7aa9-49c1-b22d-f3bcb53851dd" />

<img width="380" height="302" alt="image" src="https://github.com/user-attachments/assets/8a1d81d0-6424-4c1e-87e6-139ebf910fa0" />
2.Merge the R, G, B channels and display:

<img width="527" height="422" alt="image" src="https://github.com/user-attachments/assets/c1600662-e91e-41d5-bfa0-939682279448" />
3.Split the image into H, S, V components and display:

<img width="346" height="296" alt="image" src="https://github.com/user-attachments/assets/4e23ce6b-9f9f-43ac-9ec7-f8762c5e1ac2" />

<img width="362" height="605" alt="image" src="https://github.com/user-attachments/assets/cd6d4baa-63d0-4cf2-8d3b-9e8da82b2e6b" />
4.Merge the H, S, V channels and display:

<img width="990" height="425" alt="image" src="https://github.com/user-attachments/assets/98fccc9e-fb96-4a02-9fe1-003e4960c2af" />

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

