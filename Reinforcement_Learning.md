# Reinforcement Learning

### What is Reinforcement Learning？
- Rewards provide a positive reinforcement to our actions.
- Reinforcement Learning (RL) is the science of decision making. It is about learning the optimal behavior in an environment to obtain maximum reward.

![](Pictures/rl01.png)

- Goal directed learning from interaction
- Feedback in the form of rewards
- Agent must (learn to) act so as to maximize expected rewards
- Learning is based on observed samples of outcomes

#### Characteristics of Reinforcement Learning

- Unlike other forms of supervised learning
    - No supervisor showing the best action to take
    - Actions affect observations - agent decides based on its past observations

- Sequential decisions - time matters!
- Feedback is often delayed

### RL Applications
- Automated vehicle control (e.g  drones)
- Game playing
    - Playing Atari(雅达利) games, Tetris(俄罗斯方块), etc.
- Medical treatment
    - Planning a sequence of treatments based on the effect of past treatments
- Chat bots(e.g. Siri, Alexa,...)
    - Learning the right thing to say at the right time

### MDP Formulation

![](Pictures/rl02.png)

### RL Formulation
- Still assume a Markov Decision Process(MDP):
    - State space S
        - all possible states that an RL agent can encounter in the environment. The state space defines the universe of situations or configurations that the agent can perceive and interact with during its decision-making process.
    - Action space A
        - In Reinforcement Learning (RL), the "action space," denoted as "A," is the set of all possible actions that an RL agent can take in a given state of the environment. 
    - Environment Transition model T
    - Reward Function R
        - a "reward" is a numerical value or signal that an RL agent receives from its environment in response to the actions it takes. The reward serves as feedback to the agent, indicating how well it is performing in achieving its goals. The primary purpose of rewards in RL is to guide the learning process and help the agent make decisions that lead to desirable outcomes.
        - A reward function in Reinforcement Learning (RL) is a mathematical function or rule that quantifies the desirability or quality of the outcomes achieved by an RL agent in a specific state of the environment. It assigns a numerical reward value to each state-action pair, indicating how favorable or unfavorable the agent's behavior is in that particular situation.

- Still looking for a policy $\pi(s)$

- In RL, new twist: don't know T or R, so:
    - we don't know which states are good or what the actions do 
    - Agent must actually try actions and states to learn

- Goal: find the optimal policy that maximizes expected rewards
    - Recall the principle of maximum expected utility:

$$\pi^*(s) = \arg \max_a \sum_{s'}p(s'|s,a)U(s')$$

    - Where U(s) satisfies Bellman optimality equation:

$$U(s)=R(s)+\gamma \max_a \sum_{s'}p(s'|s,a)U(s')$$

### Bellman Equation
- "The utility of a state is the immediate reward for that state plus the expected discounted utility of the next state"

![](Pictures/DecisionMaking04.png)

$$U(s)=R(s)+\gamma \max_a \sum_{s'}p(s'|s,a)U(s')$$

- R(S): immediate reward
- $\gamma \max_a \sum_{s'}p(s'|s,a)U(s')$ : discounted expected utility of the next state, assuming optimal action

$$p(s'|s,a)=T(s,a,s')$$

![](Pictures/rl03.png)

![](Pictures/rl04.png)


### Model-Based Learning
- Key intuition:
    - Learn an approximate model based on experience
    - Solve for values as if the learned model were correct
    - After learning, the agent can make predictions about **T** and **R** before taking action 

- Step 1: Learn empirical MDP 
    - Count outcomes s' for each s, a $\hat{T}(s,a,s')$
    - Normalize to give an estimate of $\hat{T}$
    - Discover each $\hat{R}(s,a,s')$ when we experience(s,a,s')

- Step 2: Solve the learned MDP
    - For example, use value iteration, as before

### Model-Based Learning: Example

![](Pictures/rl05.png)

- Advantage:
    - Make good use of data

- Disadvantage:
    - Requires building the sctual MDP model
    - Intractable if state space is too large

### Model-Free Learning
- Remember: we don't know the transition model **T** and reward distribution **R**

Key intuition: Learn while optimizing policy

- Model is unknown but agent observes samples
- Adjust "model" as you observe more samples
- Learn optimal policy by sampling the environment(without the need to create a model beforehand)

#### Differences:
- Model-free reinforcement learning is a category of reinforcement learning algorithms that do not require a model of the environment to operate. Model-free algorithms learn directly from experience or trial-and-error and use the feedback they receive to update their internal policies or value functions. Model-free algorithms operate in the absence of complete knowledge of the environment dynamics or a transition model.
- Model-based reinforcement learning is a category of reinforcement learning algorithms that require a model of the environment to operate. Model-based algorithms learn the dynamics of the environment from experience and use the learned model to predict the outcomes of actions.

![](Pictures/rl06.png)

### Passive Reinforcement Learning
![](Pictures/rl07.png)

Simplified task: policy evaluation
- Input: a fixed policy $\pi(s)$
- We don't know the transitions T(s,a,s')
- We don't know the rewards R(s,a,s')
- Goal: learn the state values

In this case:
- No choice about what actions to take
- Just executr the policy and learn from experience
- Learned values depend on the policy
(is $pi(s)$ is "bad", the values won't be very useful)

### Temporal Difference(TD) Learning

Key idea: 
- Update V(s) each time we experience a transition(s,a,s',r)
- Likely outcomes s' will contribute more often

Temporal Difference learning of values:
- Policy still fixed, still doing evaluation!
- Move values toward value of whatever successor occurs: running average

**Sample pf V(s):**

$$sample = R(s,\pi(s),s')+\gamma V^{\pi}(s')$$

**Update to V(s):**

$$V^{\pi}(s)\gets (1-\alpha)V^{\pi}(s)+(\alpha)sample$$

**Same Update:**

$$V^{\pi}(s)\gets V^{\pi}(s)+\alpha(sample-V^{\pi}(s))$$

- sample: waht actually did happen(in one experience)

- $V^{\pi}(s)$ : what we thought would happen


##### TD Learning Example

![](Pictures/rl08.png)

![](Pictures/rl09.png)

![](Pictures/rl10.png)

![](Pictures/rl11.png)

![](Pictures/rl12.png)

![](Pictures/rl13.png)