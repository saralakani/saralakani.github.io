---
layout: post
title: Techniques for ML Model Validation, Monitoring and Tuning
#subtitle: 
#cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/validation.png
#share-img: /assets/img/path.jpg
tags: [Model Validation, Model Performance, Model tuning, Machine learning, Supervised Learning]
usemathjax: true
---

In all machine learning models, there is ways to check whether your model is working as expected. There are standardized ways to validate the model and if needed, tune it up. It is required to emphasis here on the importance of deviding data into three categories of Traininf, cross-validation and test set, to be able to benchmark the performance of your model. The rule of thumb is to assign the larger portion to training set and dedive the reamainings equaly between cross-validation and test data sets, an example woulde be 60% training, and 20% test and cross-validation each. 


1- Cost function vs iterations. For gradient-descent based models, the general validation method is to check if cost function is decreasing against the increment of iterations.

2- The Learning Curve. In this method we are trying to find out if the training set size is large enough to provide us with a reliable model or not. In this regard we need to run our training algorithm several times with various training set sizes. Then, we plot the error of cross-validation data set against the size of training set that our model has been trained on. In the same plot we want to draw the error of training set. Analysis on the behaviour of these two trends against each other is a good guage for tuning the model parameters and improve the performance. Before diving into details of learning curve validation, I first explain two main deficiencies that ML models often suffer from; High Bias and High variance.

* High Variance: This deficiency is also known as Overfitting. As a reminder, overfitting means our model is too fitted for the training set that it cannot do a good job on test data set. This problem can happen when

  * We have too many features 
  * We have too many hidden layers (in case of neural networks)  
  * We have too many polynomial terms in our feature vector
  * Our raining set is not large enough; this also called a low-bias model

  To remedy the issue of too many features, there are couple of approaches:

  * Reducing features using feature-selection algorithms.
  * Keep the features but apply Regularizing method.
        
  Note: Regularization is a way to reduce the magnitude of parameters( known as weights in some contexts) in ML models. The regularization variable known as \(lambda\) is  multiplied to the sum of squared of model parameters and the final product is added to the cost function, where we call it a regularized cost function.

  Chosing a good \(lambda\) can be a bit tricky and needs some validation approaches. Choosing a too large \(lambda\) value can lead to underfitting while too small (lambda\) may not help with overfitting.


* High Bias: This deficiency is also known as Underfitting and is the opossite of high variance situations. To remedy this issue we can apply one of the following approaches
  * Increase the number of features. One of such methods is known as "feature Mapping". the method is to add polynomial terms of your current features. For example if you have only two features \({x_1,x_2}\) you can introduce powers and polinomial terms and increase number of feature like \({x_1,x_2,x_1x_2,x_1^2,x_2^2,x_1x_2^2,x_2x_1^2,...}\).
  * Adding mode hidden layers


3- Plotting the decision boundary.

* If you observed the decision boundry is not linear, you can use feature mapping to introduce non-linear features.

4- Model accuracy: squared mean of error

5- Confusion Matrix. This matrix help us to gaugae the performance of our model, specifically when using logistic regression and we want to tune the threshold of activation function. In this appraoch we need to populate the confucion matrix each time we tune the threshold. Then we can calculate the Precision (sensitivity) and recall (specificity) values and accordingly the \(F_1\)-Score, as defined below.


|                | Real True      | Real False    |
|----------------|----------------|---------------|
| **Predicted True** | True Positive (tp)  | False Positive (fp)|
|**Predicted False** | False Negative (fn) | True Negative |

The \(F_1\) score is computed using precision (prec) and recall (rec):

{% raw %}
  $$F_1 = \frac{2 ( prec)(rec)}{prec + rec}$$

  where        

  $$prec = \frac{tp}{tp + fp}$$
  $$rec = \frac{tp}{tp + fn}$$
{% endraw %}

Now, what if we have a imbalanced data set? Example, a data set of emails where we have spams one in 100 emails. Which evaluation method is helpful here?