# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Program:

```
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
# Load the Face Image
faceimage=cv2.imread("C:\gokul important details\SCL_0648 copy (1).jpg")
plt.imshow(faceimage[:,:,::-1]);plt.title("face")
```

![image](https://github.com
```
faceimage.shape
```
![iage](https://github.com/user-attachments/assets/febca43a-bfce-4a1f-9156-d61ffae88f9c)

```
#resized_faceImage.shape
faceimage.shape
```
![image](https://github.com/user-attachments/assets/9fb44966-74d3-4331-a9fc-121f1e8fdaf7)

```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glasspng=cv2.imread('sun.png',-1)
plt.imshow(glasspng[:,:,::-1]);plt.title("GLASSPNG")
```
![image](https://github.com/user-attachments/assets/80367f8a-d91f-48e1-9193-922a1e57a2c5)
```
# Resize the image to fit over the eye region
glasspng=cv2.resize(glasspng,(170,80))
print("image Dimension={}".format(glasspng.shape))
```
![image](https://github.com/user-attachments/assets/aa65a2c7-2299-435d-b304-3d4b69fdd647)
```
# Separate the Color and alpha channels
glassbgr=glasspng[:,:,0:3]
glassmask1=glasspng[:,:,3]
```
```
# Display the images for clarity
plt.figure(figsize=[10,10])
plt.subplot(121);plt.imshow(glassbgr[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassmask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
![image](https://github.com/user-attachments/assets/99fbdf7c-da7d-4221-849c-90473dbaa992)
```
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
facewithglassesnaive=faceimage.copy()
```
```
# Replace the eye region with the sunglass image
facewithglassesnaive[150:230, 125:295]=glassbgr
plt.imshow(facewithglassesnaive[...,::-1])
```
![iage](https://github.com/use
```
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassmask=cv2.merge((glassmask1,glassmask1,glassmask1))
```
```
# Make the values [0,1] since we are using arithmetic operations
glassmask=np.uint8(glassmask/255)

# Make a copy
facewithglassesarithmetic=faceimage.copy()

# Get the eye region from the face image
eyeroi=facewithglassesarithmetic[150:230,125:295]
maskedeye=cv2.multiply(eyeroi,(1-  glassmask))

# Use the mask to create the masked eye region
maskedglass=cv2.multiply(glassbgr,glassmask)

# Use the mask to create the masked sunglass region
eyeroifinal=cv2.add(maskedeye,maskedglass)

# Display the intermediate results
plt.figure(figsize=[10,10])
plt.subplot(131);plt.imshow(maskedeye[...,::-1]);plt.title("masked eye region")
plt.subplot(132);plt.imshow(maskedglass[...,::-1]);plt.title("masked sunglass region")
plt.subplot(133);plt.imshow(eyeroifinal[...,::-1]);plt.title("augmented eye and sunglass")
```
![image](https://github.com/user-attachments/assets/7a7c06af-c6af-443a-8b91-3c0d422227a4)
```
# Replace the eye ROI with the output from the previous section
facewithglassesarithmetic[150:230,125:295]=eyeroifinal

# Display the final result
plt.figure(figsize=[10,10]);
plt.subplot(121);plt.imshow(faceimage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(facewithglassesarithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
!image](https://github.com/user-attachments/assets/e4bc84da-50e4-4eec-9606-062c07af430f)


## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!