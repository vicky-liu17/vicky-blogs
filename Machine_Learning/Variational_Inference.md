# Variance Inference

### Maximum Likelihood(ML) and Posterior Predictive
- ML
     - Estimate $\theta_{ML}$ from training data D and then use $y(x, \theta_{ML})$
- Bayesian
    - Estimate a posterior distribution over $\theta$ based on D and then use

$$\int y(x,\theta)p(\theta|\mathcal{D})d\theta$$

### Variational Bayes-Mean Field

![](Pictures/Variational01.png)

- Variational Bayes(VB)
    - Technique for approximating a posterior


### KL-Divergence

KL divergence, short for Kullback-Leibler divergence, is a measure of how one probability distribution diverges from a second, expected probability distribution. It is used to quantify the difference between two probability distributions and is a fundamental concept in information theory.


For two discrete probability distributions P and Q over the same sample space, the KL divergence from Q to P is defined as:

$$D_{\text{KL}}(P || Q) = \sum_{i} P(i) \log\left(\frac{P(i)}{Q(i)}\right)$$

For continuous distributions, the sum is replaced by an integral.


For two discrete probability distributions P and Q over the same sample space, the KL divergence from Q to P is defined as:

$$D_{\text{KL}}(P || Q) = \sum_{i} P(i) \log\left(\frac{P(i)}{Q(i)}\right)$$

For continuous distributions, the sum is replaced by an integral.

Key points about KL divergence:

1. **Non-negativity:** $D_{\text{KL}}(P || Q) \geq 0$. It is always non-negative, and it is equal to zero if and only if P and Q are the same distribution.

2. **Not symmetric:** $D_{\text{KL}}(P || Q) \neq D_{\text{KL}}(Q || P)$ . In other words, the order of the arguments matters.

3. **Interpretation:** $D_{\text{KL}}(P || Q)$ can be interpreted as the extra amount of information, in average bits, needed to encode data from P using the optimal code for Q.

4. **Not a metric:** KL divergence is not a true metric because it does not satisfy the triangle inequality.
