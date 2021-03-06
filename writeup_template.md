# **Traffic Sign Recognition** 

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/visualization.jpg "Visualization"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./examples/placeholder.png "Traffic Sign 1"
[image5]: ./examples/placeholder.png "Traffic Sign 2"
[image6]: ./examples/placeholder.png "Traffic Sign 3"
[image7]: ./examples/placeholder.png "Traffic Sign 4"
[image8]: ./examples/placeholder.png "Traffic Sign 5"

You're reading it! and here is a link to my [project code](Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (32,32,3)
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing the traffic sign counts
![bar plot](/visualisation/sign_counts.png)

Random images from training set
![random](/visualisation/random.png)
### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because since th eiages have no color signifiance we can change the image to grayscale reducing the channel having few parameters.

As a last step, I normalized the image data because reducing the intensity of the pixel values.
![grayscale](/visualisation/gray.png)

#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Grayscale image   							| 
| Convolution 5x5     	| 1x1 stride, same padding, outputs 28x28x16 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x16 				|
| Convolution 5x5	    | 1x1 stride, same padding, outputs 10x10x32 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x32 				|
| Flatten		|          									|
| Fully connected		| input 800, output 350    								 |
| Dropout		| keep_prob 0.8          									|
| Fully connected		| input 350, output 150    									|
| Fully connected		| input 150, output 43    									|
| softmax |           |
#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

The code for training the model is in cell 11,12 and 13.  
- Epochs = 25
- Learning Rate - 0.01
- Batch size =128

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* validation set accuracy of 94%
* test set accuracy of 93%

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?
- The model was adapted from LeNet architecture. IT was able to classify Traffic Signs with an accuracy of 86%.
* What were some problems with the initial architecture?
- The architecture was able to solve recognizing handwriting is >98%, whereas the model  does not cross more than 90%
* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.
- Filter depth has been increased to capture more content from images like shapes etc. The filter dpeth applied are 16 and 32. 
- Added Dropout to prevent overfitting which further increased accuracy to 94%
* Which parameters were tuned? How were they adjusted and why?
- Epochs = 25
- Learning Rate - 0.01
More the epochs, the model can learn further and draw insights, increasing accuracy.
* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model?
- The images were convertes to grayscale, to reduce the number of parameters, as color is not required to classify signs.
- Convolution neural network reduces the number of parameters to be used. 
- I think I can further increase the model accuracy, work on the classifer further, which would make me get familiarised with the dropout, fine tuning of parameters, applying convolutions.
### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text](/new/arrow.png) ![alt text](/new/rightarrow.png) ![alt text](/new/image.png)
![alt text](/new/speed30.png) ![alt text](/new/truck.png)

The images are needed to be resized to (32,32,3), applied grayscale and normalized before feeding to the model

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Right-of-way at the next intersection     		| Right-of-way at the next intersection   									| 
| Turn right ahead    			| Turn right ahead								|
| Speed limit (30km/h)			| Speed limit (30km/h)									|
| Keep right     		|Keep right				 				|
| Vehicles over 3.5 metric tons prohibited		| Vehicles over 3.5 metric tons prohibited    							|


The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100%. 

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

![softmax](/visualisation/softmax_1.png). 
![softmax](/visualisation/softmax_2.png). 
![softmax](/visualisation/softmax_3.png). 
![softmax](/visualisation/softmax_4.png). 
![softmax](/visualisation/softmax_5.png). 




