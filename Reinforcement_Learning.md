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

Model-Based Learning: Example

