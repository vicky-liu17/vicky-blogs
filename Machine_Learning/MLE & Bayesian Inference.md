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

$$Bin(x|N,\mu) \stackrel{\Delta}{=} \binom{N}{x}\mu^x(1-\mu)^{N-x}$$

where $\binom{N}{k}\stackrel{\Delta}{=}\frac{N!}{(N-k)!k!}$ is the number of ways to choose k items from N(that is known as the binomial coefficient, and is pronounced "N choose k"). If N = 1, the binomial distribution reduces to Bernoulli distribution.

##### Categorical and multinomial distributions

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

### MLE & MAP

- Frequentist(频率学派) - Maximum Likelihood Estimation(MLE,最大似然估计)
- Bayesian(贝叶斯学派) - Maximum A Posterior(MAP, 最大后验估计)

- 频率学派与贝叶斯学派对世界的认知有本质的不同：频率学派认为世界是确定，是一个本体，这个本体的真值是不变的，我们的目标就是要找到这个真值或真值所在的范围；而贝叶斯学派认为世界是不确定的，人们对世界先有一个预判，然后通过观测数据对这个预判做调整，目标是找到最优的描述这个世界的概率分布。

- 在对事物建模时，用 $\theta$ 表示模型的参数。注意，解决问题的本质就是求 $\theta$ 。那么：
    - 频率学派，存在唯一真值 $\theta$ 。我们用 $P(head)$ 来表示硬币的bias。抛一枚硬币100次，有20次正面朝上，要估计抛硬币正面朝上的bias $P(head)=\theta$ 。在频率学派看来， $\theta$ = 20/100 =0.2, 很直观。当数据趋于无穷的时候，这种方法能给出精准的估计。然而缺乏数据时则可能产生严重的偏颇。
    - 贝叶斯学派， $\theta$  是一个随机变量，符合一定概率分布。在贝叶斯学派里有两大输入和一大输出，输入是先验(prior)和似然(likelihood)，输出是后验(posterior)。
        - 先验，即 $P(\theta)$ , 即没有观测到任何数据时，对 $\theta$ 的预先判断，例如给我一个硬币，一种可行的先验是认为这个硬币很大概率是均匀的，有很小的概率是不均匀的；
        - 似然，即 $P(X|\theta)$ ,即假设 $\theta$ 已知后我们观测到的数据应该是什么样子的
        - 后验, 即 $(\theta|X)$ ,即最终的参数分布。
    - 贝叶斯估计的基础是贝叶斯公式，如下：

$$ P(\theta|X)=\frac{P(X|\theta)P(\theta)}{P(X)}$$

- 以抛硬币为例，对一枚均匀硬币抛五次得到五次正面，如果先验认为大概率下这个硬币是均匀分布（例如最大值取在0.5处的beta分布），那么 P(head），即 $P(\theta|X)$ 是一个distribution，最大值会介于0.5-1之间，而不是武断地 $\theta=1$ 
    - 随着数据量增加，参数分布会越来越向数据靠拢，先验的影响力会越来越少。
    - 如果先验是uniform distribution，那么贝叶斯方法等价于频率方法，因为直观上讲，先验是uniform distribution本质上对事物没有任何预判。

### MLE - 最大似然估计

- Maximum Likelihood Estimation, MLE是频率学派常用的估计方法
- 假设数据 $x_1, x_2, ..., x_n$是i.i.d.的一组抽样， $X=(x_1, x_2, ..., x_n)$, 其中i.i.d表示independent and identical distribution，独立同分布（每个变量的概率分布相同，且这些随机变量相互独立）。那么MLE对 $\theta$ 的估计方法可以如下推导：

$$\hat{\theta}_{MLE} = \arg\max P(X;\theta)$$

(the expression $\hat{\theta}_{MLE} = \arg\max P(X;\theta)$ tells you that the Maximum Likelihood Estimation for the parameter $\theta$ is the value of $\theta$ that maximizes the likelihood function, making the observed data X most probable. MLE is a method for finding the parameter value that best explains the observed data based on the assumed statistical model.)

$$=\arg\max P(x_1;\theta)P(x_2;\theta)...P(x_n;\theta)$$

$$=\arg\max\log\prod_{i=1}^{n}P(x_i;\theta)$$

$$=\arg\max\sum_{i=1}^{n} \log P(x_i;\theta)$$

$$=\arg\min - \sum_{i=1}^{n}\log P(x_i;\theta)$$

- 最后一行函数被称为Negative Log Likelihood(NLL)


### MAP - 最大后验估计

- Maximum A Posteriori

- 假设数据 $x_1, x_2, ..., x_n$ 是i.i.d的一组抽样，$X=(x_1,x_2,...,x_n)$ 。那么MAP对 $\theta$ 的估计方法可以如下推导：

$$\hat{\theta}_{MLE}=\arg\max P(\theta|X)$$

$$=\arg\min -\log P(\theta|X)$$

$$=\arg\min - \log P(X|\theta) - \log P(\theta) + \log P(X)$$

(贝叶斯定理)

$$=\arg\min - \log P(X|\theta) - \log P(\theta)$$

- (P(X)可以丢掉，因为与 $\theta$ 无关)

- 注意， $-log P(X|\theta)$ 其实就是NLL，所以MLE和MAP在优化时的不同就是在于先验项 $-\log P(\theta)$


### Poisson Distribution

- Now suppose the state space is the set of all non-negative integers, so X $\in$ {0,1,2,...}. We say that a random variable has a **Poisson** distribution with parameter $\lambda >0$ , written $X ~ Poi(\lambda)$ , if its pmf(probability mass function) is 

$$Poi(x|\lambda) = e^{-\lambda} \frac{\lambda^x}{x!}$$

where $\lambda$ is the mean (and variance) of x. (The first term is just the normalization constant, required to ensure the distribution sum to 1). The Poisson distribution is often used as a model for counts of rare events like radioactive decay and traffic accidents. 

$$Bin(x|N,\mu) \stackrel{\Delta}{=} \binom{N}{x}\mu^x(1-\mu)^{N-x}$$

when $\mu \to 0$ , $n \to \infty$ , $n \mu = \lambda$ , $\mu = \lambda /n$ , binomial distribution becomes Poisson distribution. 

 $$\binom{N}{x}\mu^x(1-\mu)^{N-x} = \frac{N!}{x!(N-x)!} \cdot \frac{\lambda^x}{N^x} \cdot (1 - \frac{\lambda}{N})^{N-x}$$

 $$\lim_{N \to \infty } \frac{N!}{x!(N-x)!} \cdot \frac{\lambda^x}{N^x} \cdot (1 - \frac{\lambda}{N})^{N-x}$$

 $$= \lim_{N \to \infty } \frac{(N-1)(N-2)...(N-x+1)}{x!} \cdot \frac{\lambda^x}{N^x} \cdot (1 - \frac{\lambda}{N})^{N-x}$$

 $$\lim_{N \to \infty } \frac{(N-1)(N-2)...(N-x+1)}{N^x} = \lim_{N \to \infty } 1 \cdot (1-\frac{1}{n})(1-\frac{2}{n})...(1-\frac{x-1}{n}) = 1$$

 As a result:

 $$\lim_{N \to \infty } \frac{(N-1)(N-2)...(N-x+1)}{x!} \cdot \frac{\lambda^x}{N^x} \cdot (1 - \frac{\lambda}{N})^{N-x} = \frac{\lambda^x}{x!}\cdot (1 - \frac{\lambda}{N})^{N-x}$$

Meanwhile:

 $$\lim_{N \to \infty}(1 - \frac{\lambda}{N})^{N-x} = \lim_{N \to \infty}(1 - \frac{\lambda}{N})^{N}(1 - \frac{\lambda}{N})^{-x}=\lim_{N \to \infty}(1 - \frac{\lambda}{N})^{N}$$

 According to 

 $$\lim_{x \to \infty}(1+\frac{1}{x})^x = e$$

Then

$$\lim_{N \to \infty}(1 - \frac{\lambda}{N})^{N} =\lim_{N \to \infty}[(1 + \frac{1}{-\frac{N}{\lambda}})^{- \frac{N}{\lambda}}]^{-\lambda} = e^{-\lambda}$$

$$\lim_{N \to \infty }{\lambda^x}{x!}\cdot (1 - \frac{\lambda}{N})^{N-x} = e^{-\lambda} \frac{\lambda^k}{k!}$$
