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