---
layout : post
title : AI01, Loading and manipulating images with keras
categories: [AI01]
comments : true
tags : [AI01]
---
[Back to the previous page](https://userdyk-github.github.io/Study.html) <br>
List of posts to read before reading this article
- <a href='https://userdyk-github.github.io/'>post1</a>
- <a href='https://userdyk-github.github.io/'>post2</a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

## Contents
{:.no_toc}

* ToC
{:toc}

<hr class="division1">

## **How to Load an Image with Keras**

```python
# example of loading an image with the Keras API
from keras.preprocessing.image import load_img

# load the image
img = load_img('beach.jpg')

# report details about the image
print(type(img))
print(img.format)
print(img.mode)
print(img.size)

# show the image
img.show()
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<p>
  <class 'PIL.JpegImagePlugin.JpegImageFile'><br>
  JPEG<br>
  RGB<br>
  (640, 427)
</p>
![beach](https://user-images.githubusercontent.com/52376448/63721646-9e666c80-c88c-11e9-97ee-096cc2a4f9d1.jpg)
<hr class='division3'>
</details>

<br><br><br>

### ***Argument1 : grayscale***
```python
# example of loading an image with the Keras API
from keras.preprocessing.image import load_img

# load the image
img = load_img('beach.jpg', grayscale=True)
print(img.mode)
img
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<p>
  L
</p>
![다운로드](https://user-images.githubusercontent.com/52376448/63721802-f8ffc880-c88c-11e9-9c03-5999a37ca43b.png)
<hr class='division3'>
</details>

<br><br><br>

---

### ***Argument2 : color_mode***

```python
# example of loading an image with the Keras API
from keras.preprocessing.image import load_img

# load the image
img = load_img('beach.jpg', color_mode='rgba')
print(img.mode)
img
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<p>RGBA</p>
![다운로드 (1)](https://user-images.githubusercontent.com/52376448/63722390-0e292700-c88e-11e9-800d-dcdef10fbacc.png)
<hr class='division3'>
</details>

<br><br><br>

---

### ***Argument3 : target_size***

```python
# example of loading an image with the Keras API
from keras.preprocessing.image import load_img

# load the image
img = load_img('beach.jpg', target_size=(100,100))
print(img.size)
img
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<p>(100, 100)</p>
![다운로드 (2)](https://user-images.githubusercontent.com/52376448/63722417-1b461600-c88e-11e9-957d-5ba8aae1318b.png)
<hr class='division3'>
</details>

<br><br><br>


<hr class="division2">


## **How to Convert an Image With Keras**

```python
# example of converting an image with the Keras API
from keras.preprocessing.image import load_img
from keras.preprocessing.image import img_to_array
from keras.preprocessing.image import array_to_img
import numpy as np
from PIL import Image

# load the image
img = load_img('beach.jpg')
print(type(img))

# convert to numpy array
img_ndarray = np.asarray(img).astype('float32')
img_array = img_to_array(img)
print(img_ndarray.dtype)
print(img_ndarray.shape)
print(img_array.dtype)
print(img_array.shape)

# convert back to image
img_pil1 = array_to_img(img_array)
img_pil2 = img_array.astype(np.uint8)
img_pil2 = Image.fromarray(img_pil2)
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<p>
  <class 'PIL.JpegImagePlugin.JpegImageFile'><br>
  float32<br>
  (427, 640, 3)<br>
  float32<br>
  (427, 640, 3)
</p>
<hr class='division3'>
</details>

<br>

```python
print(type(img_ndarray))
print(img_ndarray.shape)
img_ndarray
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<p>
  <class 'numpy.ndarray'><br>
  (427, 640, 3)
</p>
```
array([[[ 47., 107., 195.],
        [ 47., 107., 195.],
        [ 46., 106., 194.],
        ...,
        [ 31.,  97., 191.],
        [ 30.,  96., 190.],
        [ 29.,  95., 189.]],

       [[ 46., 106., 194.],
        [ 47., 107., 195.],
        [ 47., 107., 195.],
        ...,
        [ 31.,  97., 191.],
        [ 31.,  97., 191.],
        [ 30.,  96., 190.]],

       [[ 46., 106., 194.],
        [ 48., 108., 196.],
        [ 51., 108., 197.],
        ...,
        [ 30.,  96., 190.],
        [ 31.,  97., 191.],
        [ 30.,  96., 190.]],

       ...,

       [[  1.,   1.,   3.],
        [  1.,   1.,   3.],
        [  3.,   3.,   1.],
        ...,
        [130., 149., 155.],
        [136., 155., 161.],
        [135., 152., 160.]],

       [[  0.,   1.,   0.],
        [  1.,   2.,   0.],
        [  1.,   2.,   0.],
        ...,
        [123., 143., 144.],
        [129., 148., 152.],
        [131., 148., 155.]],

       [[  1.,   0.,   5.],
        [  0.,   0.,   4.],
        [  0.,   1.,   0.],
        ...,
        [122., 142., 141.],
        [126., 146., 145.],
        [129., 147., 149.]]], dtype=float32)
```
<hr class='division3'>
</details>

<br>

```python
print(type(img_array))
print(img_array.shape)
img_array
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<p>
  <class 'numpy.ndarray'><br>
  (427, 640, 3)
</p>
```
array([[[ 47., 107., 195.],
        [ 47., 107., 195.],
        [ 46., 106., 194.],
        ...,
        [ 31.,  97., 191.],
        [ 30.,  96., 190.],
        [ 29.,  95., 189.]],

       [[ 46., 106., 194.],
        [ 47., 107., 195.],
        [ 47., 107., 195.],
        ...,
        [ 31.,  97., 191.],
        [ 31.,  97., 191.],
        [ 30.,  96., 190.]],

       [[ 46., 106., 194.],
        [ 48., 108., 196.],
        [ 51., 108., 197.],
        ...,
        [ 30.,  96., 190.],
        [ 31.,  97., 191.],
        [ 30.,  96., 190.]],

       ...,

       [[  1.,   1.,   3.],
        [  1.,   1.,   3.],
        [  3.,   3.,   1.],
        ...,
        [130., 149., 155.],
        [136., 155., 161.],
        [135., 152., 160.]],

       [[  0.,   1.,   0.],
        [  1.,   2.,   0.],
        [  1.,   2.,   0.],
        ...,
        [123., 143., 144.],
        [129., 148., 152.],
        [131., 148., 155.]],

       [[  1.,   0.,   5.],
        [  0.,   0.,   4.],
        [  0.,   1.,   0.],
        ...,
        [122., 142., 141.],
        [126., 146., 145.],
        [129., 147., 149.]]], dtype=float32)
```
<hr class='division3'>
</details>

<br>

```python
print(type(img_pil1))
print(img_pil1.format) 
print(img_pil1.mode)
print(img_pil1.size)
img_pil1
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<p>
  <class 'PIL.Image.Image'><br>
  None<br>
  RGB<br>
  (640, 427)
</p>  
![다운로드 (3)](https://user-images.githubusercontent.com/52376448/63722987-585ed800-c88f-11e9-8edf-586712ad87d1.png)
<hr class='division3'>
</details>

<br>

```python
print(type(img_pil2))
print(img_pil2.format) 
print(img_pil2.mode)
print(img_pil2.size)
img_pil2
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<p>
  <class 'PIL.Image.Image'><br>
  None<br>
  RGB<br>
  (640, 427)
</p>  
![다운로드 (4)](https://user-images.githubusercontent.com/52376448/63723086-9825bf80-c88f-11e9-8a45-e1e28158a1db.png)
<hr class='division3'>
</details>

<br><br><br>

<hr class="division2">


## **How to Save an Image With Keras**

```python
# example of saving an image with the Keras API
from keras.preprocessing.image import load_img
from keras.preprocessing.image import save_img
from keras.preprocessing.image import img_to_array

# load image as as grayscale
img = load_img('beach.jpg', color_mode='grayscale')

# convert image to a numpy array
img_array = img_to_array(img)

# save the image with a new filename
save_img('bondi_beach_grayscale.jpg', img_array)

# load the image to confirm it was saved correctly
img = load_img('bondi_beach_grayscale.jpg')
print(type(img))
print(img.format)
print(img.mode)
print(img.size)
img.show()
```
<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<p>
  <class 'PIL.Image.Image'><br>
  None<br>
  RGB<br>
  (640, 427)
</p>
![bondi_beach_grayscale](https://user-images.githubusercontent.com/52376448/63722526-50526880-c88e-11e9-98b3-d8bc432be018.jpg)
<hr class='division3'>
</details>

<br><br><br>


<hr class="division1">

List of posts followed by this article
- [post1](https://userdyk-github.github.io/)
- <a href='https://userdyk-github.github.io/'>post2</a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

Reference
- [post1](https://userdyk-github.github.io/)
- <a href='https://userdyk-github.github.io/'>post2</a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>
<hr class='division3'>
</details>
