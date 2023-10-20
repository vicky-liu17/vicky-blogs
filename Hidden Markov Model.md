# Hidden Markov Model

### What is Markov Model?
- A Markov model is a stochastic method for randomly changing systems that possess the Markov property. This means that, at any given time, the next state is only dependent on the current state and is independent of anything in the past.

### Two commonly applied types of Markov model
- **Markov chains**: These are the simplest type of Markov model and are used to represent systems where all states are observable. Markov chains show all possible states, and between states, they show the transition rate, which is the probability of moving from one state to another per unit of time. 
- **Hidden Markov Model**：
    - A hidden Markov model (HMM) is a statistical Markov model in which the system being modeled is assumed to be a Markov process (referred to as X) with unobservable ("hidden") states. As part of the definition, HMM requires that there be an observable process Y whose outcomes are "influenced" by the outcomes of X in a known way.
    - Given the knowledge of the hidden state $X_{t-1}$, the current hidden state $X_t$ is independent of all past hidden states $X_{\tau}$, with $\tau\lt t-1$. Similarly, given the current state $X-t$ the current observation $O_t$ is independent of all past states and observations. 
    - Equiped with this notation, we can define the joint probability of a sequence of made observations $o_{1:T}$ and all hidden states in the time interval $[1, T]$ as:
    
    $$P(O_{1:T}=o_{1:T}, X_{1:T})=P(X_1)P(O_1=o_1|X_1)\prod_{t=2}^{T}P(X_t|X_{t-1})P(O_t=o_t|X_t)$$

    - Since the hidden states are unknown to use, they must be modeled under uncertainty. This is achieved by modeling the probability distribution over the transition from one state to another and the probability distribution over the observations given the current state. 
    - Thus, $P(X_t = x_t|X_{t−1} = x_{t−1})$ denotes the probability of being in a specific state at time t given that the system was in a specific state at time $t-1$. $P(O_t = o_t | X_t = x_t)$ is the probability of observing $o_t$ given that the system is in hidden state $x_t$.

    - At each time step $t\in[1,T]$ in the interval from 1 to $T$ an HMM can be characterized by the following components:
        - $X_t = x_i$, $i\in${1,2,...N}: N possible hidden states
        - $O_t = o_k$, $k\in${1,2,...N}: K possible observations
        - $\pi_{i}=P(X_1=i)$: The initial probability vector $\pi\in\mathbb{R}^{1,N}$ with elements $\pi_{i}$
        - $a_{i,j}=P(X_{t+1}=j|X_{t}=i)$: The transition probability matrix $A\in\mathbb{R}^{N,N}$ with elements $a_{i,j}$
        - $b_{i}(k)=P(O_t=k|X_t=i)$:the observation probability matrix $B\in\mathbb{R}^{N,K}$ with elements $b_{i,k}=b_i(k)$
        - The transition probability matrix A describe the probability of being in state j at time t+1 given that the system has been in state i at time t. Equivalently, the observation probability matrix B describes the probability of observing k at time t given that the system is in state i at time t. 

### HMMs can be cast into different problem settings
- Evaluating/Filtering: Compute likelihood $p(O_{1:t}|\lambda)$ of observation sequence $(O_{1:T}={O_1, O_2,...O_t,...,O_T})$ given $\lambda$. 
    - **Forward Algorithm**
- Decoding: Most likely state sequence $X_{1:T}^*$ given $O_{1:T}$ and $\lambda$.
    - **Viterbi algorithm**
- Learning: Estimate model parameters $\Lambda={\lambda}$ given $O_{1:T}$ such that $P(O_{1:T}|\lambda)$ is maximized. $\to$ A and B matrices and $\pi$. 
    - **Baum–Welch Algorithm**

- In general terms, let $O\sim P(O)$ and $X\sim P(X)$ be random variables in a discrete space that can take values $O\in{{o_1,o_2,...o_n}}$