## Vehicle Detection Project

In this project a software pipeline is designed to identify vehicles in a video from a front-facing camera on a car.

Tools Used: `python (sci-kit-learn, cv2)`.

[Link](https://youtu.be/ydAGYtD5oaU) to the output of this project.

[//]: # (Image References)

[image1]: ./examples/car_not_car.png "Visualization of images"
[image2]: ./examples/HOG_example.jpg "Hog features"
[image3]: ./examples/pipeline.jpg "Pipeline"

## Steps followed in the project

* I started by reading in all the `vehicle` and `non-vehicle` images.  Here is an example of one of each of the `vehicle` and `non-vehicle` classes:

  ![alt text][image1]

* I then explored different color spaces and different `skimage.hog()` parameters (`orientations`, `pixels_per_cell`, and `cells_per_block`).  I grabbed random images from each of the two classes and displayed them to get a feel for what the `skimage.hog()` output looks like. Here is an example using the `YCrCb` color space and HOG parameters of `orientations=8`, `pixels_per_cell=(8, 8)` and `cells_per_block=(2, 2)`:

  ![alt text][image2]

  Finalized parameters are shown in the table:

| finalized Parameters         		|     Values	        					|
        |:---------------------:|:---------------------------------------------:|
        | orientations         		| 9  							|
        | pixels_per_cell      	| (8,8)	|
        | cell_per_block					|		(2,2)										|
        | spatial_size	      	| (32,32)			|
        | color_space      	| YCrCb 	|

* I tried various choice of parameters and highest training accuracy is achieved when all the features are used (i.e. hog and color). Feature extraction is done in the code cell 5.

* I trained a linear SVM (in code cell 6) using HOG features along with color features (spatial and histogram). Data set is split into 80% training set and 20% test set to validate the accuracy of the classifier. Accuracy of the classifier is 98.9%.

* Variable sliding window is used to find if a car is present in the area window. I experimented with scales and y_start_stop values in the code cell 9 and finalized them for the video pipeline in cell 10. Working of pipeline on test images provided is shown the figure 3. First image shows positive detections, followed by heatmap and thresholding. Lablels for the thresholded heat map is created in 4th image using scipy.ndimage.measurements.label() which is followed by drawing bounding boxes in 5th image.

  ![alt text][image3]
