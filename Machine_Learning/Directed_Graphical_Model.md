# Directed Graphical Model

## Introduction
- A graphical model is a probabilistic model for which the conditional independence structure in encoded in a graph. In a graphical model, vertices(or nodes) represent randon variables, and the edges encode conditional independence relations among the associated vertices. 
- Directed Graphical Models: the edges of the graph have directions(arrows).

![](Pictures/DGM01.png)

### The definition of conditional independence

Let X, Y and Z be random variables. X and Y are conditionally independent given Z, written X ⫫ Y| Z, if

$$p(x,y|z)=p(x|z)p(y|z)$$

for all x, y and z.

- This means that, once Z is known, Y provided no extra information about X. An equivalent definition is that p(x|y,z)=p(x|y) for all x, y and z. 

## Directed Acyclic Graphs(DAGs)

- A directed graph G consists of a set of vertices V and an edge set E of ordered pairs of vertices. 

- If an arrow connects two variables X and Y (in either direction) we say that X and Y are **adjacent**. If there is an arrow form X to Y then X is a **parent** of Y and Y is a **child** of X. 
- The set of all parents of X is denoted by $\pi_X$ or $\pi(x)$.
- X is an ancestor of Y if there is a directed path from X to Y(or X=Y). We also say that Y is a descendant of X.

![](Pictures/DGM02.png)

- The collider property is path dependent. In Figure 18.4. Y is a collider on the path {X,Y,Z} but it is a non-collider on the path {X,Y,W}

![](Pictures/DGM03.png)

- 