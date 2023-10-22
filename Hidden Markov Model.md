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

- In general terms, let $O\sim P(O)$ and $X\sim P(X)$ be random variables in a discrete space that can take values $O\in \{o_1,o_2,...o_k\}$ and $X\in \{x_1,x_2,...x_k\}$ respectively. The joint probability distribution over O and X is denoted by P(O,X) and the conditional distribution of O given X by P(O|X).

- The marginal probability mass distribution of $P(O=o_i)$ is given by 
$$P(O=o_i)=\sum_{j=1}^{m}P(O=o_i,X=x_j)=\sum_{j=1}^{m}P(O=o_i|X=x_j)P(X=x_j)$$

### HMM 1 - Probability of Observation Sequence
- We want to estimate what the probability of the made observation sequence $O_{1:t} = [O_1 = 0_1, O_2=o_2, ..., O_T=o_T]$ is . In order to solve this problem, we can make use of the so-called forward algorithm or α-pass algorithm. This procedure iteratively estimate the probability to be in a certain state i at time t and having observed the observation sequence up to time t for t∈[1, ..,T]

- Brute-force method
$$P(O_1:t)=\sum_{X_1:t}P(O_1:t,X_1:t)=\sum_{X_1:t}P(O_1:t|X_1:t)P(X_1:t)$$
$$=\sum_{X_1:t}\pi a_{1,2}a_{2,3}...a_{T-1,T}b_{x_1}(O_1)b_{x_2}(O_2)...b_{x_T}(O_T)$$

- Time Complexity
    - We need to summing over all possible permutations of $X_{1:T}$
    - Evaluating this requires $O(TN^T)$ multiplications:
        - Exhaustively enumerate all state chains (t time steps)
        - In every step, there are N possible hidden states
        - There are totally $N^T$ possiblities
        - When you calculating every possible state chain, there are T steps(You need to calculate from the beginning to the end for every chain), and the complexity is O(T).
        - Totally: $O(TN^T)$

### Forward Algorithm:

- Introduce $\alpha$
- Given hidden state x=i, we call the probability of the observation sequence is ${0_q, o_2,..., o_t} forward probability. 
$$\alpha_t(i) = p(O_{1:t},x_t=i|\lambda)=P(O_1=o_1|X_1=x_i)P(X_1=x_i)=b_i(o_i)\pi_i$$



