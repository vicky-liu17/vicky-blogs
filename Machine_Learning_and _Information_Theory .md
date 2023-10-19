# Machine Learning & Information Theory

### What is Information Theory？
- Information theory is a scientific field that studies the encoding, compression, transmission of digital information.

##### What is information?
- Intuitively, we could describe information as “new knowledge”, an observation of something that we didn’t already know. Moreover, something we already know does not provide any new information.
>  For example, if I tell you that the coin landed either heads or tails, you would probably think that I was wasting your time, since that is something that you probably took for granted. Conversely, a rare event can provide a lot of information: if the coin landed on its edge instead, that would certainly be news to you. 
> Similarly, we usually have a vague expectation of what type of e-mails that may have landed in our mailbox since the last time we checked it. A booking confirmation is a much more boring e-mail than the last-minute announcement of a surprise lecture in this course by a world-class machine-learning researcher.

##### How suprised am I that outcome x happen?
- The **information content** of an outcome $x$ measures this amount of surprise. Formally, it is defined as a function of the probability, as follows:
$$h(x)=log\frac{1}{P(x)}=-logP(x)$$
- The quantity is also known as the **Shannon information**(after its inventor) or the **surprisal**. 

![](Pictures/InformationTheory01.png)

- The mathematical expression above has the following three desirable properties:
    - Property 1: The information content has a monotonic relationship with probability.
    > In particular, less probable things should have more information content, since they are more surprising when they happen.
    - Property 2: A guaranteed event has zero information content.
    > This is also intuitive. As discussed above, we are not surprised at all when an event that has a 100% probability to happen actually happens.
    - Property 3: The information content of a joint outcome $(x,y)$ of two independent random variables $\pmb x, \pmb y$ is the sum of the information content of the two individual outcomes. 
    > This property means that if two events are completely independent from each other, then we don’t gain or lose any extra information by observing them at the same time.
- **There are many functions that satisfy at least one of the above conditions. However, it turns out that the negative logarithm is the only function that satisfies all three of them, making it the perfect choice as a function to represent information content.**

###### Prove property 3 of the Shannon information content:
$$h(x,y) = -logP(x,y)=-log(P(x)\cdot P(y))=-logP(x)-logP(y)=h(x)+h(y)$$

### Entropy
- In practice, we are often more interested in entire distributions rather than single outcomes.For example, it is useful to ask how informative the e-mails in our inbox tend to be, on average. 
- The information entropy (also called the Shannon entropy) is a natural generalisation of the information content to a discrete random variable $\mathrm{\pmb x}$. It is defined as the expected information content across all possible outcomes:
$$H(x)=\mathbb{E}_{x\sim \mathcal{P}_x}[h(x)]= - \sum_{x \in \Omega}$$