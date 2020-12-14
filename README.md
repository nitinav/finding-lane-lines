# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I converted the image to grayscale, then applied gaussian blur to it, and then detected edges using canny. A region of interest was then defined using the shape of the image (video frame). After this, the hough transform step was done, and this step includes line drawing. In the end, the original image and the hough lines were overlayed to product the final image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
1. Splitting the line segments into left and right lanes. Line segments with slopes that are too horizontal or too vertical were ignored.
2. For both left and right segments, cv2.fitLine was used with the FAIR distance function to get the most robust line. I decided to use this approach rather than simply averaging and extrapolating the points and slopes (the approach that was suggested in the course).
3. This line was then averaged with the last few lines (up to 10) from previous frames for better smoothness between frames. This was also not required in the course, but improved the results.
4. The averaged line was finally drawn

Output images can be found in folder "test_images_output"
Similarly, output videos are in "test_videos_output"

### 2. Identify potential shortcomings with your current pipeline

1. This pipeline can only deal with image/video of daytime.
2. This pipeline assumes that there's nothing (with edges of similar slope to lanes) right in front of the car
3. This pipeline didn't perform very well on the challenge video, probably because of different colors and curved lanes


### 3. Suggest possible improvements to your pipeline

1. Some lines were still drawn not exactly over the lanes (even after using cv2.getLine and averaging with last 10 lines). This needs to be fixed.
2. Handle "potential shortcoming" scenarios identified above.