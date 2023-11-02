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

where $\mu = \mathbb{E}= p(x=1) is the mean.

If x counts the number of heads in N trials, we can use the binomial distribution:

$$Bin(x|N,\mu) \stackrel{\Delta}{=} \binom{N}{x}\mu^x(1-\mu)^(N-x)$$

where $\binom{N}{k}\stackrel{\Delta}{=}\frac{N!}{(N-k)!k!}$ is the number of ways to choose k items from N(that is known as the binomial coefficient, and is pronounced "N choose k"). If N = 1, the binomial distribution reduces to Bernoulli distribution.

