## Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
* Detects the face in an image.
* Places a stylish sunglass overlay perfectly on the face.
* Works seamlessly with individual passport-size photos.
* Customizable for different sunglasses styles or photo types.

  
## Technologies Used:
* Python.
* OpenCV for image processing.
* Numpy for array manipulations.


## How to Use:
* Clone this repository.
* Add your passport-sized photo to the images folder.
* Run the script to see your "cool" transformation!


## Applications:
* Learning basic image processing techniques.
* Adding flair to your photos for fun.
* Practicing computer vision workflows.

## Program:

## Developed By: Syed Shamsheer Ali .B

## Register Number:  212225220114

## Import Required Libraries:
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

## Import Original Face:
```
img = cv2.imread(r'C:\Users\syedf\OneDrive\Documents\DIPT\Syed1.png')
if img is not None:
    plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
    plt.title("Face")
    plt.axis('off')
    plt.show()
else:
    print("Image not found!")
```

## Display Glass PNG:
```
print(img.shape)
faceImage = cv2.imread(r'C:\Users\syedf\OneDrive\Documents\DIPT\Syed1.png')
print(faceImage.shape if faceImage is not None else "Image not found!")
```

```
glassPNG = cv2.imread(r'C:\Users\syedf\OneDrive\Documents\DIPT\sunglass.png', -1)
if glassPNG is not None:
    plt.imshow(cv2.cvtColor(glassPNG, cv2.COLOR_BGRA2RGBA));
    plt.title("glassPNG"); 
    plt.axis('off'); 
    plt.show()
else:
    print("Image not found!")
```

## Display Sunglass Color Channels and Sunglass Alpha Channels:
```
glassPNG = cv2.resize(glassPNG,(190,50))
print("image Dimension ={}".format(glassPNG.shape))
```

```
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```

```
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```

## Display The Original Face With Sunglass:
```
img = cv2.imread(r'C:\Users\syedf\OneDrive\Documents\DIPT\Syed1.png')
glassPNG = cv2.imread(r'C:\Users\syedf\OneDrive\Documents\DIPT\sunglass.png', -1)

w = 300; h = int(glassPNG.shape[0]*w/glassPNG.shape[1])
glass = cv2.resize(glassPNG, (w, h))
x, y = 370, 450
roi = img[y:y+h, x:x+w]; a = glass[:,:,3:4]/255
img[y:y+h, x:x+w] = (glass[:,:,:3]*a + roi*(1-a)).astype('uint8')

plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)); plt.axis('off'); plt.show()
```

## Display the Masked Eye Region, Masked Sunglass Region and Augmented Eye and Sunglass:
```
glassMask = np.uint8(cv2.merge((glassMask1,)*3)/255)
faceWithGlassesArithmetic = faceImage.copy()
eyeROI = faceWithGlassesArithmetic[135:185,110:300]
maskedEye = cv2.multiply(eyeROI, 1-glassMask)
maskedGlass = cv2.multiply(glassBGR, glassMask)
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

plt.figure(figsize=[20,20])
for i,(im,t) in enumerate([(maskedEye,"Masked Eye Region"),(maskedGlass,"Masked Sunglass Region"),(eyeRoiFinal,"Augmented Eye and Sunglass")],1):
    plt.subplot(1,3,i); plt.imshow(im[...,::-1]); plt.title(t)
```

## Display the Original Image and original Image With Sunglass:
```
faceWithGlassesArithmetic[135:185,110:300] = eyeRoiFinal
plt.figure(figsize=[10,10])
plt.subplot(121); plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image")
plt.subplot(122); plt.imshow(faceWithGlassesArithmetic[:,:,::-1]); plt.title("With Sunglasses")

w=320; h=int(glassBGR.shape[0]*w/glassBGR.shape[1])
glass=cv2.resize(glassBGR,(w,h))
mask=cv2.merge([cv2.resize(glassMask1,(w,h),interpolation=cv2.INTER_NEAREST).astype(np.float32)/255]*3)
x,y=350,450; out=faceImage.copy(); roi=out[y:y+h,x:x+w]
out[y:y+h,x:x+w]=(roi*(1-mask)+glass*mask).astype(np.uint8)

plt.imshow(cv2.cvtColor(out,cv2.COLOR_BGR2RGB)); plt.title("With Sunglasses"); plt.axis('off'); plt.show()
```

## Output:

## Import Original Face:

<img width="367" height="511" alt="{6B84C7E9-5180-41D2-9577-855CFC9D8810}" src="https://github.com/user-attachments/assets/33e6fb6b-390b-4907-9cda-12bd84360133" />

## Display Glass PNG:

<img width="659" height="344" alt="{85EB1A60-C0E3-4D81-BD48-24F7B0302193}" src="https://github.com/user-attachments/assets/def544df-68d6-4c8b-968f-0fb9db1569de" />

## Display Sunglass Color Channels and Sunglass Alpha Channels:

<img width="1380" height="256" alt="image" src="https://github.com/user-attachments/assets/fbef5a67-87ef-4e26-b53d-45502bb82a23" />

## Display The Original Face With Sunglass:

<img width="364" height="467" alt="{56573CD3-BC0D-488B-9777-4BBC15852B8B}" src="https://github.com/user-attachments/assets/a3b7d873-86ed-4a9a-9cea-592f1bb2d3ff" />

## Display the Masked Eye Region, Masked Sunglass Region and Augmented Eye and Sunglass:

<img width="1364" height="177" alt="{C6A7508F-102A-46C6-84B0-325058176AD6}" src="https://github.com/user-attachments/assets/dfac58d4-213a-4055-9b39-78535c4c96d0" />

## Display the Original Image and original Image With Sunglass:

<img width="1070" height="662" alt="{7F151624-F87B-4BA7-8322-217AA2E796B4}" src="https://github.com/user-attachments/assets/ebf298c4-a113-4b05-a77c-363596cfb395" />

## Result:

Thus the workshop was successfully completed
