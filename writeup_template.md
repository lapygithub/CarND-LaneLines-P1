# **Finding Lane Lines on the Road** 

---

The goals / steps of this project are the following:
  * Make a pipeline that finds lane lines on the road
  * Reflect on your work in a written report


[//]: # (Image References)

[image0]: ./test_images/vid_in_2017-07-22_194955.jpg "Original"
[image1]: ./ll_images/grayscale_vid_in_2017-07-22_194955.jpg "Grayscale"
[image2]: ./ll_images/acny_vid_in_2017-07-22_194955.jpg "Canny"
[image3]: ./ll_images/amask_vid_in_2017-07-22_194955.jpg "ROI Mask"
[image4]: ./ll_images/ll_vid_in_2017-07-22_194955.jpg "Lane Lines"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I used a kernel size of 7 Gaussian blur, followed by using Canny edge detection, then masking the edges in an area of interest and finally creating a line-only image with Hough line detection.  The line detected image was merged as a transparent overlay onto the original image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calculating the positive and negatives slopes, disgarding slopes with an absolute value less than 0.55, averaged the remaining lines using cvs2.fitLine() and then clipping the lines to the area of interest polygon using cv2.clipLine().

See the images below in order - Original, Grayscale, Canny, ROI Mask, Lane Lines; 

![alt text][image0]
![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the lane lines are obscured by direct sun light on the windshield or by snow.  Additionally, lane lines might have been removed from the road for construction.

Another shortcoming could be the horizon or region of interest shifts from the currently hardcoded positions.

Lastly, there is a far amount of jitter ith curved lanes in the distance.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to find the horizon and region of interest polygon on an image by images basis.

Another potential improvement could be to smooth the frame to frame lane line differences by averaging between frames.
