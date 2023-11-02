## Week 3

### Motivation

![](Pictures/Classification01.png)

![](Pictures/Classification02.png)


### Logistic Regression
- Linear regression is not a good choice for classification problmes

![](Pictures/Classification03.png)

- when z becomes very large (e.g. 100), the Sigmoid function of z is going to be very close to 1. 

![](Pictures/Classification04.png)

- Interpretation of logistic regression output

$$f_{\overrightarrow{w},b}(\overrightarrow{x}) = \frac{1}{1+e^{-(\overrightarrow{w}\overrightarrow{x}+b)}}$$

- Meaning: "probability" that class is 1
- Example:
    - x is "tumor size"
    - y is 0 (not malignant) or 1 (malignant)

- $f_{\overrightarrow{w},b}(\overrightarrow{x}) = 0.7$
    - 70% chance that y is 1

$$f_{\overrightarrow{w},b}(\overrightarrow{x}) = P(y=1|\overrightarrow{x};\overrightarrow{w},b)$$

- probability that y is 1, given input $\overrightarrow{x}$, parameters $\overrightarrow{w}$, b.
- P(y=0)+P(y=1)=1

#### Decision Boundary

![](Pictures/Classification05.png)

![](Pictures/Classification06.png)

![](Pictures/Classification07.png)

![](Pictures/Classification08.png) 

#### Simplified loss function

![](Pictures/Classification09.png) 

![](Pictures/Classification10.png) 

- maximum likelihood


### Training logistic regression
- Find $\overrightarrow{w}$ , b
- Given new $\overrightarrow{x}$ , output $f_{\overrightarrow{w},b}(\overrightarrow{x})=\frac{1}{1+e^{-(\overrightarrow{w}\cdot\overrightarrow{x}+b)}}$

![](Pictures/Classification11.png) 

![](Pictures/Classification12.png) 

### The Problem of overfitting

![](Pictures/Overfit01.png) 

![](Pictures/Overfit02.png) 

- Technically we say that you want your learning algorithm to generalize well, which means to make good predictions even on brand new examples that it has never seen before.

### Address Overfitting

![](Pictures/Overfit03.png) 

![](Pictures/Overfit04.png) 

![](Pictures/Overfit05.png) 

- Options:
    - Collect more data
    - Select features
        - Feature selection
    - Reduce size of parameters
        - "Regularization"

![](Pictures/Overfit06.png) 

![](Pictures/Overfit07.png) 

-  what you want is some value of lambda that is in between that more appropriately balances these first and second terms of trading off, minimizing the mean squared error and keeping the parameters small.

![](Pictures/Overfit08.png) 

![](Pictures/Overfit09.png) 

![](Pictures/Overfit10.png) 