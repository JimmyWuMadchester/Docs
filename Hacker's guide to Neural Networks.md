# Hacker's guide to Neural Networks

Another study note from reading [Karpathy's blog](http://karpathy.github.io/neuralnets/) about Neural Networks.

## ToDo


## Resources

* [ConvNetJS](https://cs.stanford.edu/people/karpathy/convnetjs/)
* [Stanford's course CS231n (Convolutional Neural Networks)](http://cs231n.github.io/), and [slides](http://cs231n.stanford.edu/syllabus.html)
* [Deep Learning by Goodfellow, Bengio, and Courville](http://www.deeplearningbook.org/)

## Notes

> The majority of cost functions in Machine Learning consist of two parts: 1. A part that measures how well a model fits the data, and 2: Regularization, which measures some notion of how complex or likely a model is.

> "SIFT" & Object Recognition, David Lowe, 1999

## CS231 Course

Computer Vision Challenges:
* Viewpoint variation
* Illumination
* Deformation
* Occlusion
* Background Clutter
* Intraclass variation

### K-nearest neighbors

Hyperparameters:
* What is the best value of k to use?
* what is the best distance to use?

Chossing distance metric:
* L1 distance / Manhattan distance
* L2 distance / Euclidean distance

Chossing hyperparameters:
1. work best on the whole set of data
2. split into train and test, choose hyperparameters that work best on test data
3. split data into train, validation and test data, choose hyperparameters on 
validation set and evaluate on test data.
4. cross-validation, useful for small datasets, but not used too frequently in deep learning
 
Consider the **curse of dimensionality** when applying KNN to problems. 
The training dataset has to be densely distributed to represent the space
when predicting new outcomes. The training samples required is growing 
exponentially when the feature dimension grows. For image recognitions, it 
would be extremely difficult to have.

### SVM 

loss function: hinge loss

Regularization: used to apply preference of simpler model.
* L2 regularization: prefers sparse solutions.
* L1 regularization: trying to spread the influences across multiple inputs.
* Elastic net (L1 + L2)
* Max norm regularization
* Dropout
* Fancier: batch normalization, stochastic depth

### Softmax Classifier (Multinomial Logistic Regression)

exp -> normalize -> log

### Numerical gradient

Approximate, slow, easy to write

### Analytic gradient

exact, fast, error-prone

In practice: always use analytic gradient, but check implementation with numerical gradient.
This is called a gradient check.

### Gradient Descent

```{python}
# Vanilla Gradient Descent

while True:
  weights_grad = evaluate_gradient(loss_fun, data, weights)
  weights += - step_size * weights_grad # perform parameter update
```

### Stochastic Gradient Descent (SGD)

### Activation functions

* Sigmoid
* tanh
* ReLU
* Leaky ReLU
* Maxout
* ELU
