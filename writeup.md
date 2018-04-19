# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 7 steps. 

1. Adjust image gamma
2. Turn image into grayscale
3. Blur grayscale image
4. Find edges using Canny
5. Mask region of interest
6. Find lines in Hough space
7. Draw best guessed line

I adjust the image's gamma to reduce the negative effects from shadow and overexposed highlights in the images. This has been helpful for the challenge scenario.

After this, I followed the pipeline covered in the lecture. First turn the image into grayscale, blur and find edges, mask region of interest and then find lines in Hough space. I used similar parameters we had in the lecture.

For better visualization, I modified my `draw_lines()` function of filter out best guessed lane lines. I did this by finding the slope of all output lines from Hough space, in `x = ky + b` form, flipping `x` and `y` is to better model lines close to vertical. Then I retrieve lines within a range of slope, eg. `(-2, 2)`. Finally I did a kmean clustering in `k,b` space, where `k=2`, to find the best guess lane lines.


### 2. Identify potential shortcomings with your current pipeline


The gamma adjustments are to accommodate the challenge we have, which include many shadow and overexposes. However in most case this does not make substantial difference.

Most of the parameters are fixed for the purpose of this project. Given a different scenario these parameters may not perform well.

Kmean for best guessed lane lines could give incorrect result, since there no guarantee that the input represent both two lane lines or the clustering can correctly find two distinct cluster.


### 3. Suggest possible improvements to your pipeline

Adjust gamma based on actual exposure level of image, or the shadow/highlights curve.

Make pixel-count related parameters variable to image size. I did this for masking, but some other parameters might need this as well.

Find a better and more reliable way for averaging the lane lines. Maybe different clustering method, or cluster in different dimensions. 
