# Chapter 2 - Statistical learning.

Input variables often called predictors, independent variables, features or sometimes just variables.

Output variables are often called the response or dependent variable. (typically Y).

Supose we observe a quantitative reponse Y and p different predictors, we assume there is a relationship written in the general form
$$
Y = f(X) + \epsilon
$$

Statistical learning refers to a set of approaches for estimating $f$, as well as tools for evaluating the estimates obtained.

## Why estimate $f$?

### Prediction.

In many situations inputs X are available, but Y cannot easily be obtained. Since error term averages to 0 we can predict Y.

$\hat{Y} = \hat{f}(X)$

$\hat{f}$ represents our estimate for $f$, A $\hat{Y}$ represents the resulting prediction for Y.$\hat{f}$ is treated as a black box.

The accuracy of $\hat{Y}$ as a prediction for Y depends on two quantities, which we will call the reducible error and the irreducible error. In general $\hat{f}$ will not be a perfect estimate but is reducible by improving accuracy. Even if perfect would have error as $\epsilon$ cannot be predicted using X, this being the irreducible error. 

$$
E(Y-\hat{Y})^2
= E[f(X) + \epsilon - \hat{f}(X)]^2
= \underbrace{E[f(X) - \hat{f}(X)]^2}_{\text{Reducible}}
+ \underbrace{Var(\epsilon)}_{\text{Irreducible}}
$$

### Inference.

We are often interested in the association between Y and X values. In this situation we wish to estimate $f$, but our goal is not neccessarily to make predictions for Y.

- Which predictors are associated with the response?
- What is the relationship between reponse and each predictor?
- Can the relationship between Y and each predictor be adequately sumarised using a linear equation, or is the relationship more complicated?

Linear models allow for relatively simple and interpretable inference, but may not yield as accurate predictions. Some of the highly non-linear approaches can provide accurate $\hat{Y}$ but at the expense of less interetable model for which inference is more challenging. 

## How do we estimate $f$?

We will always assume that we have observed a set of n different data points. These observations are called training data as used to train our method to predict $f$.

Find a function such that $Y \approx \hat{f}(X)$ for any observation (X, Y).

### Parametric Methods.

2 step approach.

1. Assumption about the functional form, or shape, of $f$. E.g. that $f$ is linear. $f(X) = \beta_0 + \beta_1X_1 + ... + \beta_pX_p$
2. Then we need a procedure that uses the training data to fit or train the model. In the case of the linear model $Y \approx \beta_0 + \beta_1X_1 + ... + \beta_pX_p$. Most common approach to fitting the model is (ordinary) least squares.

Parametric reduces estimtating $f$ down to estimating a set of parameters. Downside is it will often not match true unknown form of $f$. If chosen model is too far from true $f$, then our estimates will be poor. We can address this by chosing a more flexible model but in general fitting a more flexible model requires estimating a greater number of parameters which can lead to overfitting where they follow the errors, or noise too closely.

### Non-Parametric Methods.

Non-parametric do not make explicit assumptions about the functional form. They seek an estimate of f that gets as close to the data points without being too rough or wiggly. Can potentially fit a wider range of possible shapes for $f$ by avoiding assumptions. Parametric estimate of $f$ can be very different from $f$. As non-parametric do not reduce the problem of estimating to a small number of parameters, a large number of observations is required to estimate $f$ accurately.

### Trade-off between Prediction Accuracy and Model Interpretability.

In general, as the flexibility of a method increases, its interpredtability decreases.
When inference is the goal, there are clear advantages to using simple and relatively inflexibile statistatical learning methods. When only interested in prediction interpretability is not of interest.

### Supervised Versus Unsupervised Learning.

Majority of the book is Supervised learning.
With unsupervised learning we lack a response variable that can supervise our analysis. Cluser analysis or clustering can be used on the basis of the variables measured to identify groups. It might be that them groups differ with respect to some property of interest.
Semi-supervised when not all responses are measured, often due to responses being more expensive to collect. This is beyond the scope of this book.

### Regression Versus Classification Problems.

Quantitative variables take on a numerical value. Qualitative variables take on values in one of K different classes, or categories. We tend to refer to problems with a quantatative response as regression problems, while those with a qualitative response as classification problem. Logistic regression is a classification method despite the name, typical use with a qualitative response, as it estimates class probabilities it can be thought as regression also.

## Assessing Model Accuracy.

### Measuring the Quality of Fit.

In the regression setting, the most commonly-used measure is the mean squared error (MSE), given by  MSE
$$
MSE = \frac{1}{n}
\sum_{i=1}^{n}
(y_i - \hat{f}(x_i))^2
$$
Where $\hat{f}(x_i)$ is the predictor that $\hat{f}$ gives for the ith observation. MSE will be small if predicted response is close. MSE computed using the training data used to fit the model so should be referred to as the training MSE.

We are not interested if $\hat{f} \approx y_i$ instead we want to know if $\hat{f}(x_0) \approx y_0$, where $(x_0, y_0) is a previously unseen test observation not used to train the statistical learning method. Choose method with lowest test MSE not lowest training MSE.

If we have large number of test observations can compute
$$
Ave(y_0 - \hat(x_0))^2
$$
The average squared prediction error for these test observations $(x_0, y_0)$.

If no test observations you may think selecting the SL method with minimised training MSE but there is no guarantee it will produce the lowest test MSE. As many statistical methods estimate coefficients so to minimize the training set MSE. For these methods, the training set MSE can be quite small, but the test MSE is often much larger.

Regrardless of overfitting, we almost always expect the training MSE to be smaller than the test MSE as most methods either directly or indirectly seek to minimize the training MSE. Overfitting refers to when a less flexible method would have yielded a smaller test MSE.

### The Bias-Variance Trade-off

Expected test MSE, for a given $x_0$ can be decomposed into the sum of the variance of $\hat{f}(x_0)$, the squared bias of $\hat{f}(x_0)$ and the variance of the error term $\epsilon$.

$E(y_0 - \hat{f}(x_0))^2 = Var(\hat{f}(x_0)) + [Bias(\hat{f}(x_0))]^2 + Var(\epsilon)$

$E(y_0 - \hat{f}(x_0))^2$ defines the expected test MSE at $x_0$, and refers to the average test MSE that we would obtain if we repeatedly estimated $f$ using a large number of training sets, and tested each at $x_0$. OVerall expected test MSE can be computed by averaging $E(y_0 - \hat{f}(x_0))^2$ over all possible values of $x_0$ in the test set.

To minimise test error we need a method that gives low variance and low bias. cannot go below the irreducible error as variance and bias are non-negative.

If large variance small changes in training data can change $\hat{f}$ a lot. Higher flexibilty in the method generally have higher variance.

Variance refers to the amount $\hat{f}$ would change if we used a different training data set.
Bias referes to the error introduced by approximating a real-life problem, which may be extremely complicated, by a much simpler model. For example linear regression assumes a linear relationship which is unlikely with real-life problems which will result in bias.
Generally more flexible methods result in less bias..

As we use a more flexible method, variance increases and bias decreases. The relative rate of change of these two quantitities determines whether the test MSE increases or decreases.

As we increase the flexibility of a class of methods, the bias tends to initially decrease faster thean the variance increases. Consequently, the expected test MSE declines. However, at some point  increasing flexibility has little impact on the bias but starts to significantly increase the variance.

### The Classification Setting.

The training error rate. The proportion of mistakes that are made if we apply our estimate $\hat{f}$ to the training observations:

$$
\frac{1}{n}
\sum_{i=1}^{n}
I(y_i \not ={\hat{y_i}}).
$$

Here $\hat{y_i}$ is the predicted class label for the ith observation using $\hat{f}$. $I(y_i \not ={\hat{y_i}} )$ is an indicator value that equals 1 if $I(y_i \not ={\hat{y_i}})$ is true and 0 if false. If 0 it was classified correctly.

