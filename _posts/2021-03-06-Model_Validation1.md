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

In all machine learning models, there is ways to check whether your model is working as expected. There are standardized ways to validate the model and if needed, tune it up. It is required to emphasis here on the importance of dividing data into three categories of Training, cross-validation and test set, to be able to benchmark the performance of your model. The rule of thumb is to assign the larger portion to training set and divide the reamainings equaly between cross-validation and test data sets, an example woulde be 60% training, and 20% test and cross-validation sets each. 


1- Checking Cost function vs iterations. For gradient-descent based models, the general validation method is to validate if cost function is decreasing against the increment of iterations. Otherwise, the model needs to be corrected. For this validation method, plotiing is cost function over iterations (epochs) is a common practice.

2- Checking the Learning Curve. In this method we are trying to find out the best size for the training set. In this regard we need to run our training algorithm several times with various training set sizes. Then, we plot the error of cross-validation data set against the size of training set that our model has been trained on. In the same plot, we want to draw the error of training set as well. Analysis on the behaviour of these two trends against each other is a good guage for tuning the model parameters and improve the performance. Before diving into details of learning curve validation, I first explain two main deficiencies that ML models often suffer from; which are known as High Bias and High variance.

* High Variance: This deficiency is also known as Overfitting. As a reminder, overfitting means our model is too fitted for the training set that it cannot do a good job on test data set. This problem can happen when

  * We have too many features 
  * We have too many hidden layers (in case of neural networks)  
  * We have too many polynomial terms in our feature vector
  * Our raining set is not large enough; this also called a low-bias model

Example below shows a high variance polynomial regression model where the training error is very low but the cross-validation error is high, meaning the model is overfitting the training data.

![Learning Curve for High Variance example](/assets/img/high_variance.JPG "High Variance model example")

  To remedy the issue of too many features, there are couple of approaches:

  * Reducing features using feature-selection algorithms.
  * Keep the features but apply Regularizing method.
        
  Note: Regularization is a way to reduce the magnitude of parameters( known as weights in some contexts) in ML models. The regularization variable known as $$lambda$$ is  multiplied to the sum of squared of model parameters and the final product is added to the cost function, where we call it a regularized cost function.

  Choosing a good $$lambda$$ can be a bit tricky and needs some validation approaches. Choosing a too large $$lambda$$ value can lead to underfitting while too small $$lambda$$ may not help with overfitting.


* High Bias: This deficiency is also known as Underfitting and is the opossite of high variance situations. 
In high bias situation we often see the learning curve as below, where this particular linear regression model is too simple and is unable to fit our dataset well.

![Learning Curve for High Bias example](/assets/img/high_bias.JPG "High Bias model example")

To remedy this issue we can apply one of the following approaches
  * Increase the number of features. One of such methods is known as "feature Mapping". the method is to add polynomial terms of your current features. For example if you have only two features $${x_1,x_2}$$ you can introduce powers and polinomial terms and increase number of feature like $${x_1,x_2,x_1x_2,x_1^2,x_2^2,x_1x_2^2,x_2x_1^2,...}$$.
  * Adding mode hidden layers (in case of neural networks)


3- Plotting the decision boundary for SVM models. In classification models using _Support Vector Machine_, the idea is to find a decision boundary between classes, either linear boundary or non-linear. Plotting can be helpful to see if our classification model is doing a good job or not. You can tune _C_, namely the SVM regularization parameter, to reach the best decisison boundary. Larger _C_ tends to include more outliers inside the decision boundary however can lead to a non-optimal margin between classes.
The plot below shows linear SVM classifier where _C=1_ but there is an outlier lef out.

![Decision boundary for linear SVM for C=1](/assets/img/Linear_SVM_C1.JPG "Decision boundary for linear SVM for C=1")

And example below shows that for _C=100_ the SVM model includes the outlier but the decision boundary is not optimal.

![Decision boundary for linear SVM for C=100](/assets/img/Linear_SVM_C100.JPG "Decision boundary for linear SVM for C=100")

* If you observed the decision boundry is not optimal, you can use feature mapping to introduce non-linear features. 

4- Model accuracy: This evaluation metric is mostly implemented by calculating squared mean of error on your test data set.

5- Confusion Matrix. This matrix help us to gaugae the performance of our model, specifically when using logistic regression and we want to tune the threshold of activation function. In this appraoch we need to populate the confucion matrix each time we tune the threshold. Then we can calculate the Precision (or Positive Predictive Value) and recall (or sensitivity) values and accordingly the $$F_1$$-Score, as defined below.


|                | Real True      | Real False    |
|----------------|----------------|---------------|
| **Predicted True** | True Positive (tp)  | False Positive (fp)|
|**Predicted False** | False Negative (fn) | True Negative |

The $$F_1$$ score is computed using precision (prec) and recall (rec):

{% raw %}
  $$F_1 = \frac{2 ( prec)(rec)}{prec + rec}$$

  where        

  $$prec = \frac{tp}{tp + fp}$$

  $$rec = \frac{tp}{Real True}=\frac{tp}{tp + fn}$$
{% endraw %}

Now, what if we have a imbalanced data set? Example, a data set of emails where we have spams one in 100 emails. Which evaluation method is helpful here?

*Refrence: Machine Learning course by Andrew NG, available for free in Coursera!*