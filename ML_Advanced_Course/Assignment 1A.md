# DD2434 Assignment 1A

## 1.1 Exponential Family

A number of common distributions can be rewritten as exponential-family distributions with natural parameters, in the following form:

$$p(x|\theta) = h(x)exp(\eta(\theta)\cdot T(x) - A(\eta))$$

Below we provide five different distributions from exponential-family. Show which common distributions they correspond to.

#### Question 1.1.1:

- $\theta = \lambda$
- $\eta(\theta)=log(\theta)$
- $h(x)=\frac{1}{x!}$
- $T(x)=x$
- $A(\eta)=e^{\eta}$

##### Answer: The Poisson distribution

The expression for the probability mass function of a Poisson random variable is as follows:

$$p(x|\lambda)=\frac{\lambda^x e^{-lambda}}{x!}$$

Rewrite the expression:

$$p(x|\lambda)=\frac{1}{x!}exp{x\log\lambda - \lambda}$$

Therefore, the Poisson distribution is an exponential family distribution:

$$\eta = \log\lambda$$

$$T(x)=x$$

$$A(\eta)=\lambda=\e^{\eta}$$

$$h(x)=\frac{1}{x!}$$

