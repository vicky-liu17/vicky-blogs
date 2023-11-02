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
- Given new $\overrightarrow{x}$ , output $f_{\overrightarrow{w},b}(overrightarrow{x})=\frac{1}{1+e^{-(\overrightarrow{w}\cdot\overrightarrow{x}+b)}}$