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
[image38]: ./resources/extrapolate_line.png "Extrapolate Line"


---

## Reflection

### 1. Pipeline

My pipeline consisted of 5 steps. Most of them were learned in the lesson.

* [Color Select](#color-select)
* [Grayscale](#grayscale)
* [Smoothing With Gaussian Blur](#smoothing-with-gaussian-blur)
* [Edge Detect](#edge-detect)
* [ROI Select](#roi-select)
* [Hough Transform](#hough-transform)
* [Extrapolate line](#extrapolate-line)
* [Final Videos](#final-videos)

### 2. Color Select

I use RGB filtering by applying white and yellow mask on the image. Here are the results:

![alt text][image32]


### 3. Grayscale

After color select, I apply grayscaling on the images as shown here:

![alt text][image33]

### 4. Smoothing With Gaussian Blur

For good practice, grayscaling images should be smoothing for edge detect. I choose Gaussian Blur to smooth the images.

![alt text][image34]


### 5. Edge Detect

For edge detect, Canny Alg is a good choice.

![alt text][image35]

### 6. ROI Select

After all above steps, I have gotten edge images. Now, I want to remove the unimportant part. The sky, the hill, the tree and others are unimportant. Interest Region is defined by four vertices.

```
width = image.shape[1]
height = image.shape[0]
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

### 8. Extrapolate line

After Hough Transform, we get a collection of line segments. How to find left line and right line? I use tuple `<slope, intercept>` to indicate a line. If slope is negative, it should be a left line. If slope is positive, it should be a right line.
Through the way, we can get left lines collection and right lines colletion. The weighted average based on intercept length is applied to the two collections to find a left line and a right line.

```
def average_slope_intercept(lines):
    left_lane_lines    = [] # (slope, intercept)
    left_lane_weights  = [] # (length,)
    right_lane_lines   = [] # (slope, intercept)
    right_lane_weights = [] # (length,)
    
    for line in lines:
        for x1, y1, x2, y2 in line:
            if x2==x1:
                continue # ignore a vertical line
            slope = (y2-y1)/(x2-x1)
            intercept = y1 - slope*x1
            length = np.sqrt((y2-y1)**2+(x2-x1)**2)
            if slope < 0: # y is reversed in image
                left_lane_lines.append((slope, intercept))
                left_lane_weights.append((length))
            else:
                right_lane_lines.append((slope, intercept))
                right_lane_weights.append((length))

    # Weight slopes and Y_intercepts by their line lenght
    right_lane = np.dot(right_lane_weights, right_lane_lines) / np.sum(right_lane_weights) if len(right_lane_weights) > 0 else None
    left_lane  = np.dot(left_lane_weights,  left_lane_lines) / np.sum(left_lane_weights)  if len(left_lane_weights) > 0 else None

    return right_lane, left_lane
```

See result example:
![alt text][image38]

### 9. Final Videos

You can find videos from the link:
* [solidYellowLeft.mp4](https://github.com/liangtaohy/CarND-LaneLines-P1/tree/master/test_videos_output)
* [solidWhiteRight.mp4](https://github.com/liangtaohy/CarND-LaneLines-P1/tree/master/test_videos_output)
* [challenge.mp4](https://github.com/liangtaohy/CarND-LaneLines-P1/tree/master/test_videos_output)

## Potential shortcomings with the pipeline

* Identifying curves.
* The line quality is tested when the car is driving at higher speeds.
* I think there should be a more robust and dynamic method of identifying the road's horizon rather than just including 60% of the image height.
* Polynomial fit for lane line fit

