## Week 2

#### Multiple Features

![](Pictures/MultipleFeatures01.png)

- Model:
    - Previously: $f_{w,b}(x)=wx+b$
    - Now: $f_{w,b}(x)=w_{1}x_{1}+w_{2}x_{2}+...+b$
    - $\overrightarrow{w} = [w_1,w_2,w_3...w_n]$
    - b is a number 
    - $\overrightarrow{w}$ and b are the parameters of the model
    - $\overrightarrow{x} = [x_1,x_2,...x_n]$
    - $f(\overrightarrow{x})=\overrightarrow{w}\cdot \overrightarrow{x}+b$
    - This is multiple linear regression (not multivariate regression)
        - Linear regression with multiple features

![](Pictures/GradientDescent01.png)

![](Pictures/GradientDescent02.png)

### An alternative to gradient descent

- Normal equation
    - Only for linear regression
    - solve for w,b without iterations
    - Disadvantages:
        - Doesn't generalize to other learning algorithms
        - SLow wehn number of features is large(>10000)
    - What you need to know
        - Normal Equation Method may be used in machine learning libraries that implement linear regression
        - Gradient descent is the recommend method for finding parameters w,b

### Feature Scaling

- Feature and parameter values

$$\hat{price}=w_1x_1+w_2x_2+b$$

- $x_1$ : size ( $feet^2$ ) range 300-2000
- $x_2$ : number of bedrooms  range: 0-5

- House: $x_1$ = 2000, $x_2$ = 5, price = $500k - one training example