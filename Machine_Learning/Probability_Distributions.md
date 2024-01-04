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

Substituting the expression for $B(\alpha, \beta)$ into the PDF, we get:

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

### Exercises

1.1: Let $X = (X_1, ..., X_N)$ be i.i.d. where $X_n|P,m \sim Binomial(m,P)$ and $P \sim Beta(\alpha, \beta)$ . Show that the posterior p(P|X,m) follows a Beta-distribution, i.e. that the Beta is conjugate prior to the Binomial with known m. What are the parameters of the posterior?

Let's denote the observed data as $x = (x_1, \ldots, x_N)$, where $x_n$ is the outcome of the $n$-th trial. The likelihood function is given by the product of the individual Binomial probabilities:

$$P(x | P, m) = \prod_{n=1}^{N} \binom{m}{x_n} P^{x_n} (1 - P)^{m - x_n}$$

The prior distribution on $P$ is given by $P(P) = \text{Beta}(P | \alpha, \beta)$ .

The posterior distribution is proportional to the product of the likelihood and the prior:

$$P(P | x, m) \propto P(x | P, m) \cdot P(P)$$

Now, let's simplify this expression:

$$P(P | x, m) \propto \prod_{n=1}^{N} \binom{m}{x_n} P^{x_n} (1 - P)^{m - x_n} \cdot P^{\alpha - 1} (1 - P)^{\beta - 1}$$

Combining like terms, we get:

$$P(P | x, m) \propto P^{\sum_{n=1}^{N} x_n + \alpha - 1} (1 - P)^{N \cdot \sum_{n=1}^{N} (m-x_n) + \beta - 1}$$

This expression has the form of the kernel of a Beta distribution. By comparing with the probability density function (PDF) of the Beta distribution, we can identify the parameters of the posterior:

$$P(P | x, m) \propto \text{Beta}(P | \alpha + \sum_{n=1}^{N} x_n, \beta + N \cdot m - \sum_{n=1}^{N} x_n)$$

Therefore, the posterior distribution $P(P | x, m)$ follows a Beta distribution with parameters $\alpha + \sum_{n=1}^{N} x_n$ and $\beta + N \cdot m - \sum_{n=1}^{N} x_n$ . This confirms that the Beta distribution is indeed conjugate to the Binomial likelihood with known m.