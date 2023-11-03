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

