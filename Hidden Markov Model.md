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
- Given hidden state x=i, we call the probability of the observation sequence is ${0_q, o_2,..., o_t}$ forward probability. 
$$\alpha_1(i) = p(O_{1:t},x_t=i|\lambda)=P(O_1=o_1|X_1=x_i)P(X_1=x_i)=b_i(o_i)\pi_i$$

- At time t, we need to marginalize over the probability of having been in any other state at t-1 and multiply this estimate the matching observation probability as follows:

$$\alpha_t(i)=P(O_{1:t},X_t=x_i)$$

$$=P(O_{t}=o_t|X_t=x_i,O_{1:t-1})P(X_t=x_i, O_{1:t-1})$$

(Given the current state $X-t$ the current observation $O_t$ is independent of all past states and observations.)

$$=P(O_t=o_t|X_t=x_i)P(X_t=x_i, O_{1:t-1})$$

$$P(O_t=o_t|X_t=x_i)[\sum_{j=1}^{N}P(X_t=x_i|X_{t-1}=x_j)P(X_{t-1}=x_j, O_{1:t-1})]$$

> Maginalization is a method that requires summing over the possible values of one variable to determine the marginal contribution of another. 

- This step has to be computed iteratively for every $t\in [1,...,T]$. Finally, we can compute the probability of having observed the given observation sequence $O_1:T$. For this, we again have to marginalize over the hidden state distribution such that
$$P(O_{1:T}=o_{1:T})=\sum_{j=1}^{N}P(O_{1:T}=0_{1:T}, X_T=x_j)$$
$$=\sum_{j=1}^{N}\alpha_T(j)$$

```python
# Define the forward algorithm for Hidden Markov Models (HMMs)
def forward_algorithm(A, B, pi, O):
    # N: Number of hidden states
    N = len(A)
    
    # T: Number of time steps in the observation sequence
    T = len(O)
    
    # Initialize the matrix to store forward probabilities
    forward_probs = [[0.0] * T for _ in range(N)]
    
    # Initialization step: Calculate the initial forward probabilities
    for j in range(N):
        forward_probs[j][0] = pi[j] * B[j][O[0]]
    
    # Recursion step: Calculate forward probabilities for each time step
    for t in range(1, T):
        for j in range(N):
            # Calculate the forward probability for state j at time t
            forward_probs[j][t] = sum(forward_probs[i][t-1] * A[i][j] for i in range(N)) * B[j][O[t]]
    
    # Termination step: Sum up the forward probabilities at the last time step
    # to obtain the total probability of observing the sequence O
    probability = sum(forward_probs[i][T-1] for i in range(N))
    
    # Return the total probability of the observed sequence
    return probability
```

- The forward algorithm use a matrix to store the forward probabilities of each step. So every time, we only need to calculate from the last step(t-1) to current step(t). 
- We do not need to calculate from the very begining. In every time step, there are $N^2$ possibilities. (from j to i, j and i both have N possibilities). 
- There are totally T time steps. 
- So the time complexity of the forward algorithm is $O(N^{2T})$.

### HMM 2 - Estimate Sequence of States
- The forward algorithm marginalizes over the hidden state distribution. 
- In contrast, we can also compute the most likely sequence of hidden states given the observations.
- Let use denote this sequence with $X^*=\{ X_1, X_2, ...X_t \}$


- Given:
    - Emission Sequence $O=\{ O_1, O_2, ...O_t \}$
    - A, B, $\pi$
- To find:
    - Hidden state sequence  that most likely produce O.
    - Probability of occurrence of $X^*=\{ X_1, X_2, ...X_t \}$

#### Viterbi Algorithm
![](Pictures/hmm01.png)
- Goal: To find the shortest path from S to E.

- Start from S to A
    - There are 3 paths S-A1、S-A2、S-A3. 
    - But now we cannot arbitrarily say which path is the shortest under global conditions.
    - So we move to B.
    - There are three path passing B1.
        - S-A1-B1
        - S-A2-B1
        - S-A3-B1
    - Suppose S-A3-B1 is the shortest in the above three paths, the other two cannot be the final result, so we can delete them directly. 
    - Similarly, we can find the shortest path passing B2 and B3, and delete the other paths. 
    - We can store the length of the shortest path in a matrix, like:
        - B1: length of S-A3-B1
        - B2: length of S-A2-B2
        - B3: length of S-A2-B3
    - When we move forward, we can directly use it. 
    - We can also calculate the distance of the following points like this. 
    - In terms of efficiency, compared to roughly traversing all paths, the Viterbi algorithm will delete paths that do not meet the shortest path requirements when reaching each column, greatly reducing the time complexity.

- In HMM:
    - At first, we need to compute the probability of having observed $O_{1:t}=o_{1:t}$ and being in a state $X_t=x_i$ for each t.
$$\delta_t(i)=P(O_1=o_1,X_1=x_i)=b_i(o_1)\pi_{i}$$
    - The subsequent steps update the $\delta_t$ as follows:
$$\delta_t(i)=\max_{j\in[1,2,...,n]}P(X_t=x_i|X_{t-1}=x_j)P(O_{1:t-1},X^*_{1:t-2},X^*_{t-1})$$
In order to be alble 