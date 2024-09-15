Given a picture and a set of discrete labels, the computer will assign a label to the picture.

## Semantic Gap
Machines see the picture as a matrix of numbers, representing pixels and 3 channels RGB between 0 to 255.

Our algorithm need to be robust to situations like:
- illumination
	- different lighting conditions
- deformation
	- different poses and positions
- occlusion
	- only part of the object is exposed
- background clutter
	- object similar to the background
- intraclass variation
	- objects in different sizes. colours. ages, shapes

# Data-Driven Approach
1. Collection a dataset of images and labels
2. Use Machine Learning to train a classifier
3. Evaluate the classifier on new images

```python
def train(images, labels):
	# machine learning
	return model

def predict(model, test_images):
	# use model to predict labels
	return test_labels
```

# Nearest Neighbour
`train()` memorize all data and labels
`predict()` predict the label of the most similar training image
- it finds the most similar image from the dataset, then return the label of it

## How to Compare Two Images?
- Distance Metric
	- Manhattan Distance
	- $d_1(I_1,I_2)=\sum_P|I^P_1-I_2^P|$
![[Screenshot 2024-09-11 at 1.40.51 PM.png]]
Results in 456 differences.

## Complexity
- Train
	- O(1)
- Predict
	- O(n)

This is bad.

We want classifiers that are fast at prediction; slow for training is ok.

# K-Nearest Neighbour
![[Screenshot 2024-09-11 at 1.51.18 PM.png]]
Let's look at the first picture where K=1. This is the Nearest Neighbour Algorithm.

The isolated yellow spot is a noise for our dataset. In K=1, it causes an area being yellow, which we don't want it happen. 

You can notice the overfitting causing the finger-like edges as well.

K-Nearest Neighbour Algorithm, instead of copying label from nearest neighbour, take majority vote from K closet points. By doing so, it smoothen fingers in the boundary, and the yellow area is gone.

The whites are tie, no majority among the K-Nearest Neighbours. One may want to give it a guess between the tie.

## Distance Metric
- L1 distance
	- Manhattan
	- diamond look
- L2 distance
	- Euclidean
	- $d_2(I_1,I_2)=\sqrt{\sum_P(I^P_1-I^P_2)^2}$
	- circle look

Hint: L1 is the sum of horizontal and vertical distances, while L2 is the length of the segment between.
![[Screenshot 2024-09-11 at 2.19.56 PM.png]]
The result of L1 tend to follow the axis.

# Hyperparameter
L1 and L2, the value of k, they are all hyperparameters. We rather set them than learn them. They are very problem-dependent, thus we must try them all out and see what works best.

## Setting Hyperparameters
### Idea 1: What works best on the training data
Bad: It will not have the ability to ignore the noise.

K=1 always works perfectly on training data. But it will not perform well.

### Idea 2: Split data into Train and Test, choose what works best on Test

Bad: No idea how algorithm will perform on new data

It will select the one works the best on the Test data

### Idea 3: Split data into Train, Val, and Test, choose hyperparameters on Val and evaluate on Test

Better!

- use multiple hyperparameters on training set 
- evaluate it on the validation set 
- pick the one works best on validation set 
- run it the test set only once

The number comes from the Test set is the number telling you how your hyperparameters doing on unseen data.

Analogy: 
- Training set is the homework
- Validation set is the mock test
- Test set it the final exam

### Idea 4: K-Folds Cross-Validation
Split data into folds, try each fold as validation and average the results.

Useful for small datasets, but not used too frequently in deep learning.
- too expensive
![[Screenshot 2024-09-11 at 2.42.09 PM.png]]

## K-Nearest Neighbour on Images Never Used
- Very slow at test time
- distance metrics on pixels are not informative
- the curse of dimensionality
	- ![[Screenshot 2024-09-11 at 2.53.59 PM.png]]
	- KNN divides the feature space and classifier them. The accuracy is related to the density. Even in the same density, when the dimension grows, the number of representative points exponentially increases.

# Linear Classification

## Parametric Approach
f(x, W) where W is a set of parameters or weights
It will return 10 numbers representing scores in the 10 categories in CIFAR-10.

For CIFAR-10, 
- W is $10\times3072$
- x is $3072\times1$
- f(x,W) is $10\times1$
- b is $10\times1$
	- bias term
![[Screenshot 2024-09-11 at 3.42.12 PM.png]]
