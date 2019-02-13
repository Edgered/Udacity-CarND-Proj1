### Reflection (README.md)

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 8 steps:

1. Convert the images to grayscale 
2. Apply Gaussian Blur to smooth the image 
3. Use the Canny edge detection algorithm to extract the edges based on the strength of gradient
4. Specify the image mask to extract the region of interest
5. Adapt the Hough Transform to find the lines in the edge
6. Employ the line extrapolation for extend the result from Hough Transform within region of interest
7. Draw the lane finding result on a separated picture
8. Merge the lane finding result with the original picture and output

In order to draw a single line on the left and right lanes, I modified the _draw_lines()_ function by using it as the last step to add lines and wrote my own version of line extrapolation method since I tend to avoid modifying the given library funtions. I did not use the full provided version of Hough Transfrom as it hides the result lines within the function.

The _extrapolate_lines()_ function I wrote esentially groups the lines found by Hough Transform by two based on their relative slope. One group is the left_lines and the other is right_lines. Then I tried to find the average slope and the average midpoint for each line under its particlar group, and with the average slope and midpoint, I can reconstruct the left and right lane within the range of region of interest. Then I output the left and right lane to _draw_lines()_ for drawing the result on image, and eventually combine both lines and forms the output of lane finding pipeline.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be the accuracy. Although I have tried to toggle various parameters for Gaussian Blur, Canny Edge, Hough Transform and the range of region of interest, certain frames still messed up with the **solidYellowLeft.mp4** and all frames are completely off with the challenge video.

Another shortcoming could be the code method. Right now I only defined 2 functions in my pipeline which are bulky and not atomic. Code refactoring is perfered to make them more modular, easier to maintain and easier to debug. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be getting more familiarized with computer vision techniques. More details for how Hough transform works should be studied to make the value I chose has a solid reasoning, rather than just test and select the combination that produces best-looking result.

Due to the limited personal experiences with numpy at the moment I did not fully utilized the functionalities provided by numpy and related library. There might be a better collection of function calls that can simplify the handwritten _extrapolate_lines()_ function.
