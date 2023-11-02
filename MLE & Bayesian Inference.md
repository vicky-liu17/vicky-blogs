### Probability

##### Bernoulli and binomial distribution
- Suppose we have a binary random variable, $x \in$ {0,1}, which we can thingk of as representing the outcome of a coin toss. It is common to model such a variable using the Bernoulli distribution, which has the form

$$
P(X = x) =
\begin{cases}
    \mu & \text{if } x = 1 \\
    1 - \mu & \text{if } x = 0
\end{cases}
$$

where $\mu = \mathbb{E}= p(x=1)$ is the mean.

If x counts the number of heads in N trials, we can use the binomial distribution:

$$Bin(x|N,\mu) \stackrel{\Delta}{=} \binom{N}{x}\mu^x(1-\mu)^(N-x)$$

where $\binom{N}{k}\stackrel{\Delta}{=}\frac{N!}{(N-k)!k!}$ is the number of ways to choose k items from N(that is known as the binomial coefficient, and is pronounced "N choose k"). If N = 1, the binomial distribution reduces to Bernoulli distribution.

##### Categorical and multinomial distributions

- 将一个小球放入两个桶，记变量x为第一个桶里小球的个数，那么只有0个或1个，所以服从伯努利分布；
- 将n个小球放入两个桶，记变量x为第一个桶里小球的个数，那么最少可能有0个，最多可能有n个，所以服从二项分布；
- 将1个小球放入k个桶，记变量x为第k个桶里小球的个数，所以是一个向量，并且是one-hot形式，因为小球只能放在一个桶里面，所以是服从Categorical分布；
- 将n个小球放入k个桶，记变量x为第k个桶里小球的个数，是一个向量，并且向量元素的和为n，所以是服从多项分布。

- If the variable is discrete-valued, x $\in$ {1,...K}, we can use the categorical distribution:

$$Cat(x|\theta)\stackrel{\Delta}{=} \prod_{k=1}^{K}\theta_k^{\mathbb{I}(x=k)}$$
