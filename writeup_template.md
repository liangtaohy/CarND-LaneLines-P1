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
[image32]: ./resources/white_yellow_image.png "Color Select"
[image33]: ./resources/grayscale_image.png "Grayscale"
[image34]: ./resources/blur_image.png "Smoothing: Gaussian Blur"
[image35]: ./resources/edge_image.png "Canny Edges"
[image36]: ./resources/roi_image.png "ROI Region"
[image37]: ./resources/solid_line.png "Hough Line"


---

## Reflection

### 1. Pipeline

My pipeline consisted of 5 steps.

* Color Select
* Grayscale
* Smoothing: Gaussian Blur
* Edge Detect: Canny Detect
* ROI Region Select
* Hough Transform
* Extrapolate lines

### 2. Color Select

I use RGB filtering by applying white and yellow mask on the image. Here are the results:

![alt text][image32]


### 3. Grayscale

After color select, I apply grayscaling on the images as shown here:

![alt text][image33]

### 4. Smoothing the images

For good practice, grayscaling images should be smoothing for edge detect. I choose Gaussian Blur to smooth the images.

![alt text][image34]


### 5. Canny Edges Detect

![alt text][image35]

### 6. ROI Select

After all above steps, I have gotten edge images. Now, I want to remove the unimportant part. Interest Region is defined by for vertices.

```
v_top_left = [int(width*0.45), int(height*0.6)]
v_top_right = [int(width*0.6), int(height*0.6)]
v_bottom_left = [int(width*0.1), height-2]
v_bottom_right = [int(width*0.95), height-2]
```

Here is the results after applying it on the Canny images:

![alt text][image36]

### 7. Hough Transform

I use Hough Transform to detect lines in the images.

![alt text][image37]

