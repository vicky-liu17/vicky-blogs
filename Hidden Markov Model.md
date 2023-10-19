# Hidden Markov Model

### What is Markov Model?
- A Markov model is a stochastic method for randomly changing systems that possess the Markov property. This means that, at any given time, the next state is only dependent on the current state and is independent of anything in the past.

### Two commonly applied types of Markov model
- **Markov chains**: These are the simplest type of Markov model and are used to represent systems where all states are observable. Markov chains show all possible states, and between states, they show the transition rate, which is the probability of moving from one state to another per unit of time. 
- **Hidden Markov Model**：
    - A hidden Markov model (HMM) is a statistical Markov model in which the system being modeled is assumed to be a Markov process (referred to as X) with unobservable ("hidden") states. As part of the definition, HMM requires that there be an observable process Y whose outcomes are "influenced" by the outcomes of X in a known way.