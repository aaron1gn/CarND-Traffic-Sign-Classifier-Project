##  Build a Traffic Sign Recognition Project

---
### Load The Data

1. Load pickled data

2. Split out features and labels

3. check the dimension of the data

4. check if the number of images data is equal to the number of labels


### Data Set Summary & Exploration

I used the pandas library to calculate summary statistics of the traffic
signs data set:

| Data set           | Dimension        |
| ------------------ | ---------------- |
| training set       | 34799, 32, 32, 1 |
| validation set     | 12630, 32, 32, 1 |
| test set           | 4410, 32, 32, 1  |
| traffic sign image | 32, 32           |
| classes/labels set | 42               |



####  An exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data ...

![](https://raw.githubusercontent.com/aaron7yi/CarND-Traffic-Sign-Classifier-Project2/master/barchart.png)



![](https://raw.githubusercontent.com/aaron7yi/CarND-Traffic-Sign-Classifier-Project2/master/barchart2.png)

![](https://raw.githubusercontent.com/aaron7yi/CarND-Traffic-Sign-Classifier-Project2/master/barchart3.png)



### Pre-process the Data Set 

1. Converting the images to grayscale
2. Normalizing the datasets
3. print data dimension 


### Model Architecture

My final model consisted of the following layers:

| Layer           | Description                                | Input       | Output   |
| --------------- | ------------------------------------------ | ----------- | -------- |
| Convolution 5x5 | 1x1 stride, valid padding, RELU activation | **32x32x1** | 28x28x48 |
| Max pooling     | 2x2 stride, 2x2 window                     | 28x28x48    | 14x14x48 |
| Convolution 5x5 | 1x1 stride, valid padding, RELU activation | 14x14x48    | 10x10x96 |
| Max pooling     | 2x2 stride, 2x2 window                     | 10x10x96    | 5x5x96   |
| Flatten         | dimensions -> 1 dimension                  | 5x5x96      | 400      |
| Fully Connected | Fully Connected, RELU activation           | 400         | 120      |
| Fully Connected | Fully Connected, RELU activation           | 120         | 84       |
| Fully Connected | Fully Connected, Softmax  activation       | 84          | 43       |



| Hyperparameters | type   |
| :-------------- | :----- |
| Optimizer       | Adam   |
| Batch size      | 128    |
| learning rate   | 0.0001 |
| Epochs          | 50     |
| Dropout         | 0.5    |

### My final model results

| Training Results    | 0.998 |
| ------------------- | ----- |
| Validation Accuracy | 0.934 |
| Test Accuracy       | 0.934 |

## Discussion of turning model

1.reduce learning rate from default 0.001 to 0.0009 to help achieve a better optimization of loss entropy.

2.dropout increase from default 0.1 to 0.5 to prevent overfitting

3.Batch size still use default  128 since I use CPU instead of GPU.

4.Epochs is set up to 10 during initial training stage to save training time since the turning pointing always appeared in epoch 5/6. However,I use epoch 50 in the training to improve model accuracy.

5.Finally, I initially use several commands from OpenCV library to preprocess image data and it seem the model get some overfitting problems. Then I use data array to process image data directly, the validation accuracy & test accuracy have a significant improvement of 93% plus. (This is something that I unable to explain but I reckon the method of processing data has a great impact on model accuracy )




### Test a Model on New Images

Here are five German traffic signs that I found on the web:

![](https://raw.githubusercontent.com/aaron7yi/CarND-Traffic-Sign-Classifier-Project2/master/11.png)

![](https://raw.githubusercontent.com/aaron7yi/CarND-Traffic-Sign-Classifier-Project2/master/22.png)

![](https://raw.githubusercontent.com/aaron7yi/CarND-Traffic-Sign-Classifier-Project2/master/33.png)

![](https://raw.githubusercontent.com/aaron7yi/CarND-Traffic-Sign-Classifier-Project2/master/44.png)

![](https://raw.githubusercontent.com/aaron7yi/CarND-Traffic-Sign-Classifier-Project2/master/55.png)



Here are the results of the prediction:

|       Image        |      Predicts      |
| :----------------: | :----------------: |
| Speed Limit 50km/h | Speed Limit 50km/h |
|       Yield        |       Yield        |
|     Road works     |     Road works     |
|     Keep right     |     Keep right     |
| Children crossing  | Children crossing  |



| Probability |     Prediction     |
| :---------: | :----------------: |
|      1      | Speed Limit 50km/h |
|      1      |       Yield        |
|      1      |     Road works     |
|      1      |     Keep right     |
|      1      | Children crossing  |

#### 