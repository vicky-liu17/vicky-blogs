# Probability Distributions

#### Bernoulli and Binomial distribution

Suppose we have a binary variable, $x\in$ {0,1}, which we can think of as representing the outcome of a coin toss. It is common to model such a variable using the Bernoulli distribution, which has the form:

$$P(X = k) = \begin{cases} 
\mu & \text{if } x = 1 \\
 1 - \mu & \text{if } x = 0
\end{cases}$$

where $\mu=\mathbb{E}=p(x=1)$ is the mean. 


If x counts the numner of heads in N trials, we can use the binomial distribution:

$$Bin(x|N,\mu) \triangleq \binom{N}{x}\mu^{x}(1-\mu)^{N-x}$$

where $\binom{N}{k} \triangleq \frac{N!}{(N-k)!k!}$ is the number of ways to choose k items from N(that is known as the binomial coefficient, and is pronounced "N choose k"), if N=1, the binomial distribution reduces to Bernoulli distribution. 

#### Beta Distribution

The Beta distribution is a continuous probability distribution defined on the interval [0,1]. It is often used to model the dsitribution of random variables representing propotions or probabilities.  


###### Probability Density Function (PDF)

The probability density function (PDF) of a Beta distribution with parameters $\alpha$ and $\beta$ is given by:

$$f(x; \alpha, \beta) = \frac{x^{\alpha-1} \cdot (1 - x)^{\beta-1}}{\text{B}(\alpha, \beta)}$$

$$B(\alpha, \beta) = \frac{\Gamma(\alpha) \cdot \Gamma(\beta)}{\Gamma(\alpha + \beta)}$$

Here, $\Gamma$ denotes the gamma function. The gamma function is defined as:

$$\Gamma(n) = (n-1)!$$

Substituting the expression for \(B(\alpha, \beta)\) into the PDF, we get:

$$f(x; \alpha, \beta) = \frac{x^{\alpha-1} \cdot (1 - x)^{\beta-1} \cdot \Gamma(\alpha + \beta)}{\Gamma(\alpha) \cdot \Gamma(\beta)}$$


#### Categorical and multinomial distributions

- 将一个小球放入两个桶，记变量x为第一个桶里小球的个数，那么只有0个或1个，所以服从伯努利分布；
- 将n个小球放入两个桶，记变量x为第一个桶里小球的个数，那么最少可能有0个，最多可能有n个，所以服从二项分布；
- 将1个小球放入k个桶，记变量x为第k个桶里小球的个数，所以是一个向量，并且是one-hot形式，因为小球只能放在一个桶里面，所以是服从Categorical分布；
- 将n个小球放入k个桶，记变量x为第k个桶里小球的个数，是一个向量，并且向量元素的和为n，所以是服从多项分布。

- If the variable is discrete-valued, x $\in$ {1,...K}, we can use the categorical distribution:

$$Cat(x|\mathrm{\theta})\stackrel{\Delta}{=} \prod_{k=1}^{K}\theta_k^{\mathbb{I}(x=k)}$$

- theta is a vector
- $\theta_k$ represents the probability associated with category $k$. In the context of a categorical distribution, $\theta_k$ is the probability of the random variable $x$ being equal to category $k$.
- $\mathbb{I}(x=k)$ is an indicator function. It takes the value 1 if the condition $x=k$ is true and 0 otherwise. In this context, $\mathbb{I}(x=k)$ is used to check if the random variable $x$ is equal to category $k$.

- Alternatively, we can represent the K-valued variable x with the one hot binary vector **x**, which lets us write:

$$Cat(x|\mathrm{\theta})\stackrel{\Delta}{=} \prod_{k=1}^{K}\theta_k^{x_k}$$

- $x_k$ is the $k$-th element of the one-hot binary vector **x**. It is equal to 1 if category $k$ is the category represented by $x$, and it is 0 otherwise.

> A one-hot binary vector is a binary vector (a vector of binary values, typically 0s and 1s) where only one element is set to 1 (hot), and all other elements are set to 0 (cold). It is often used to represent categorical variables or labels in machine learning and data analysis. The "hot" element corresponds to the category or label that is being represented.

> e.g. Suppose you have a set of fruits: {Apple, Banana, Orange, Grape}. You can represent each of these fruits using a one-hot binary vector like this: 
    - Apple: [1, 0, 0, 0] (1 in the first position)
    - Banana: [0, 1, 0, 0] (1 in the second position)
    - Orange: [0, 0, 1, 0] (1 in the third position)
    - Grape: [0, 0, 0, 1] (1 in the fourth position)

- If the k'th element of **x** counts the number of time the value k is seen in $N=\sum_{k=1}^{K}x_k$ trials, then we get the **multinomial distribution** :

$$\mathcal{M}(x|N,\theta)\stackrel{\Delta}{=}\binom{N}{x_1....x_k}\prod_{k=1}^{K}\theta_k^{x_k}$$

- $\binom{N}{x_1, x_2, \ldots, x_K}$ represents the multinomial coefficient, which calculates the number of ways to arrange $N$ trials into $x_1$ for category 1, $x_2$ for category 2, and so on, up to $x_K$ for category $K$. It accounts for the different ways these counts can be distributed within the $N$ trials.
- $\prod_{k=1}^{K} \theta_k^{x_k}$ is the product term that specifies the probability of observing category $k$ exactly $x_k$ times in each individual trial.


### Conjugate priors 共轭先验

##### Bayes formula:

$$P(\theta | X) = \frac{P(X | \theta) \cdot P(\theta)}{P(X)}$$

- Prior(先验): $P(\theta)$
- Likelihood(似然): $P(X|\theta)$
- Posterior(后延): $P(\theta|X) \propto P(X | \theta) \cdot P(\theta)$


In Bayesian statistics, a prior distribution is considered conjugate to a likelihood function if the resulting posterior distribution belongs to the same family of distributions as the prior. More formally, if the prior distribution $P(\theta)$ is conjugate to the likelihood function $P(X|\theta)$, then the posterior distribution $P(\theta|X)$ also belongs to the same family of distributions as the prior.