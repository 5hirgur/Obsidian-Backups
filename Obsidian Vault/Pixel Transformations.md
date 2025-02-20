#MachineLearning #ComputerVision #MachineVision

This page describes some common algorithms and statistical techniques leveraged to perform image transformations. 

## Histogram
A histogram counts the number of occurrences of a pixel, and it's a useful tool for understanding and manipulating images. We represent the intensity values of an image using an array where the index of the array is the intensity value. 

![[Pasted image 20250204154707.png]]

Here *h* is the histogram array and *r* is the corresponding intensity value, each cell will have the number of pixels that have the intensity value corresponding to that particular index, this gives us a bar graph or a *histogram*.

# Image Transformation 


In the image below, consider an image represented by the array $f[i,j]$ a transformation $T$ is applied to it to yield a new resulting image $g[i,j]$  

![[Pasted image 20250204184204.png#center]]

Now, let us analyze how this image transformation affect this image's histogram. Image transformation is a function of change in intensity values A.K.A the change in values at the index of the image array (recall that the index is the intensity values and the values at the index are the number of pixels of that corresponding intensity value of the image).

When intensity values are changed using image transformation, values of the histogram (the pixel count) simply move to another index of intensity values in the new histogram.

For the transformation above here is the change in the histogram subject to transformation $T$ where $h_r$ is the original histogram and $h_s$ is the new histogram, post transformation.

Consider this new image transformation example: 
![[Pasted image 20250204184830.png]]

For the above transformation, here is how the change in the histogram array looks like, $r$ and $s$ are the histogram array indexes or the intensity values of the image. In the highlighted cells below notice how the intensity values of specific pixels change and are mapped to different indexes, the value of $r = 2$ resulting 3 is now mapped to $s = 5$. This means that there are 3 pixels of intensity value of 5 in the transformed image. 

![[Pasted image 20250204184905.png]]

# Image Negatives 

Image negatives is where we reverse the intensity levels of the image. We apply the following transform to reverse the intensity levels :

$$
g[i,j] = -1f[i,j] +255
$$
This can be applied as an array operation as follows : $image\_negative = -1*image+255$ 
This is an example of a resulting transformation:

Pre Transformation:

![[Pasted image 20250209131627.png#center]]

Post Transformation:

![[Pasted image 20250209131631.png#center]]

# Brightness and Contrast Adjustments

To adjust the brightness and contrast of an image, use the following simple algorithm: $g[i,j] = \alpha f[i,j] + \beta$
Here, $\alpha$ is simple contrast control and $\beta$ is simple brightness control.

![[Pasted image 20250209132344.png#center]]


