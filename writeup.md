#**Finding Lane Lines on the Road** 

---
## Overview:

The goal of this project is to make a pipeline that finds lane lines on the road using Python and OpenCV. See an example:

The pipeline will be tested on some images and videos provided by Udacity. 

Assumptions:
* Front-Center mounted camera
* Visible line on the road
* Good weather conditions

[//]: # (Image References)
[image1]: ./test_images/solidWhiteRight.jpg
[image2]: ./outputs/mask_color.jpg
[image3]: ./outputs/grayscale.jpg
[image4]: ./outputs/canny.jpg
[image5]: ./outputs/Region_of_Interest.jpg
[image6]: ./outputs/hough.jpg
[image7]: ./outputs/Output_extrapolated_lines.jpg
[image8]: ./outputs/output_images1.jpg
[image9]: ./outputs/output_images2.jpg 
[image10]: ./outputs/challenge_image.jpg 

[video1]: ./test_videos_output/white_output.mp4
[video2]: ./test_videos_output/yellow_output.mp4

---

## Reflection

###1. Describe your pipeline.

Steps:

Original Image

![alt text][image1]

#### Color selection 

Applied filtering to remove colors below threshold.

![alt text][image2]

I will keep aside this mask and use it later.

#### Convert the color image in grayscale 

![alt text][image3]


#### Use Canny for edge detection 

Applied gaussian filtering followed by Canny detector. Canny is used to detect edges. Output of Canny is not good in some cases so to enhance the results used CV dilate (for enhancement) and then erode (for noise removal)

![alt text][image4]

#### Region Of Interest Mask
Two masks: left and right trapezoidal Region Of Interest (ROI) based on the image size. Values were determined using trial and error method to get best visual representation
 
![alt text][image5]

#### Run Hough transform to detect lines  
  
![alt text][image6]

Hough transform is used to detect the edges


#### Compute lines

To extrapolate results of Hough i.e draw continuous lines, used fitline for both regions of interest. Then drew the lines on original image, like so:  

![alt text][image7]

## Results:

### Pictures
Test image results:

![alt text][image8]  
![alt text][image9] 

The original pictures are in `test_images`and the results are located in the folder `test_images_output`.


### Videos
Test videos and results:   

Location of output video files: [link to video1]![alt text][video1], [link to video2]![alt text][video2].

[link to my video result]![alt text][video1]

### Challenge

I didnt solve for the entire video but just took a frame from it and applied the pipeline to it

![alt text][image10] 

I think given time/conviction I could refine the pipeline to work with the challenge video

###2. Identify potential shortcomings with your current pipeline

* This approach could not work properly:
    * if there is bumper to bumper traffic
    * if one or more lines are missing
    * inclement weather conditions
    * very curvy roads


###3. Suggest possible improvements to your pipeline

Some possible improvements:

* Probably use the HSV space, instead of the RGB co-ordinate system
* If a edge detection is not possible, leverage averaging of past and current edges
* Smooth curves using a better filter
