# **Finding Lane Lines on the Road By liangtaohy@gmail.com** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./test_images_output/blur_image_00.jpg "Smoothing: Gaussian Blur"
[image3]: ./test_images_output/blur_image_01.jpg "Smoothing: Gaussian Blur"
[image4]: ./test_images_output/blur_image_02.jpg "Smoothing: Gaussian Blur"
[image5]: ./test_images_output/blur_image_03.jpg "Smoothing: Gaussian Blur"
[image6]: ./test_images_output/blur_image_04.jpg "Smoothing: Gaussian Blur"
[image7]: ./test_images_output/blur_image_05.jpg "Smoothing: Gaussian Blur"
[image8]: ./test_images_output/edge_image_00.jpg "Canny Edges"
[image9]: ./test_images_output/edge_image_01.jpg "Canny Edges"
[image10]: ./test_images_output/edge_image_02.jpg "Canny Edges"
[image11]: ./test_images_output/edge_image_03.jpg "Canny Edges"
[image12]: ./test_images_output/edge_image_04.jpg "Canny Edges"
[image13]: ./test_images_output/edge_image_05.jpg "Canny Edges"
[image14]: ./test_images_output/grayscale_image_00.jpg "RGB2Gray"
[image15]: ./test_images_output/grayscale_image_01.jpg "RGB2Gray"
[image16]: ./test_images_output/grayscale_image_02.jpg "RGB2Gray"
[image17]: ./test_images_output/grayscale_image_03.jpg "RGB2Gray"
[image18]: ./test_images_output/grayscale_image_04.jpg "RGB2Gray"
[image19]: ./test_images_output/grayscale_image_05.jpg "RGB2Gray"
[image20]: ./test_images_output/roi_image_00.jpg "ROI Region"
[image21]: ./test_images_output/roi_image_01.jpg "ROI Region"
[image22]: ./test_images_output/roi_image_02.jpg "ROI Region"
[image23]: ./test_images_output/roi_image_03.jpg "ROI Region"
[image24]: ./test_images_output/roi_image_04.jpg "ROI Region"
[image25]: ./test_images_output/roi_image_05.jpg "ROI Region"
[image26]: ./test_images_output/white_yellow_image_00.jpg "Color Select"
[image27]: ./test_images_output/white_yellow_image_01.jpg "Color Select"
[image28]: ./test_images_output/white_yellow_image_02.jpg "Color Select"
[image29]: ./test_images_output/white_yellow_image_03.jpg "Color Select"
[image30]: ./test_images_output/white_yellow_image_04.jpg "Color Select"
[image31]: ./test_images_output/white_yellow_image_05.jpg "Color Select"

---

## Reflection

### 1. Pipeline

My pipeline consisted of 5 steps.

* Color Select
* Grayscale
* Smoothing: Gaussian Blur
* Edge Detect: Canny Detect
* ROI Region Select
* Hough Line Detect
* Extrapolate lines

### 2. Color Select

I use RGB filtering by applying white and yellow mask on the image. Here are the results:

![alt text][image26]
![alt text][image27]
![alt text][image28]
![alt text][image29]
![alt text][image30]
![alt text][image31]


### 3. Grayscale

After color select, I apply grayscaling on the images as shown here:

![alt text][image14]
![alt text][image15]
![alt text][image16]
![alt text][image17]
![alt text][image18]
![alt text][image19]

### 4. Smoothing the images

For good practice, grayscaling images should be smoothing for edge detect. I choose Gaussian Blur to smooth the images.

![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]
![alt text][image7]


### 5. Canny Edges Detect

![alt text][image8]
![alt text][image9]
![alt text][image10]
![alt text][image11]
![alt text][image12]
![alt text][image13]

### 6. ROI Select

After all above steps, I have gotten edge images. Now, I want to remove the unimportant part. Here is the results after applying it on the Canny images:

![alt text][image20]
![alt text][image21]
![alt text][image22]
![alt text][image23]
![alt text][image24]
![alt text][image25]
