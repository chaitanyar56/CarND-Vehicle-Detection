**Vehicle Detection Project**

[//]: # (Image References)

[image1]: ./examples/car_not_car.png "Visualization of images"
[image2]: ./examples/HOG_example.jpg "Hog features"
[image3]: ./examples/pipeline.jpg "Pipeline"
---

Link to the [project file](https://github.com/chaitanyar56/CarND-Vehicle-Detection/blob/master/vehicleDetection.ipynb) ,  [helper functions](https://github.com/chaitanyar56/CarND-Vehicle-Detection/blob/master/lesson_functions.py) and the output pipeline [video](https://github.com/chaitanyar56/CarND-Vehicle-Detection/blob/master/output_images/processed_project_video.mp4)

I started by reading in all the `vehicle` and `non-vehicle` images.  Here is an example of one of each of the `vehicle` and `non-vehicle` classes:

![alt text][image1]

I then explored different color spaces and different `skimage.hog()` parameters (`orientations`, `pixels_per_cell`, and `cells_per_block`).  I grabbed random images from each of the two classes and displayed them to get a feel for what the `skimage.hog()` output looks like. Here is an example using the `YCrCb` color space and HOG parameters of `orientations=8`, `pixels_per_cell=(8, 8)` and `cells_per_block=(2, 2)`:

![alt text][image2]

Finalized parameters are shown in the table:

| finalized Parameters         		|     Values	        					|
|:---------------------:|:---------------------------------------------:|
| orientations         		| 9  							|
| pixels_per_cell      	| (8,8)	|
| cell_per_block					|		(2,2)										|
| spatial_size	      	| (32,32)			|
| color_space      	| YCrCb 	|




2. I tried various choice of parameters and highest training accuracy is achieved when all the features are used (i.e. hog and color). Feature extraction is done in the code cell 5.

3. I trained a linear SVM (in code cell 6) using HOG features along with color features (spatial and histogram). Data set is split into 80% training set and 20% test set to validate the accuracy of the classifier. Accuracy of the classifier is 98.9%.

4. Variable sliding window is used to find if a car is present in the area window. I experimented with scales and y_start_stop values in the code cell 9 and finalized them for the video pipeline in cell 10. Working of pipeline on test images provided is shown the figure 3. First image shows positive detections, followed by heatmap and thresholding. Lablels for the thresholded heat map is created in 4th image using scipy.ndimage.measurements.label() which is followed by drawing bounding boxes in 5th image.

![alt text][image3]

---
*Discussion:*
For better smooth tracking a filter can be designed to estimate the position of the car in the next frame and use that estimated frame along with the current detected frame to remove false positives. The pipeline's tracking performance depends on the speed of the vehicle, by estimating the speed and position of the adaptive window size can be used.
