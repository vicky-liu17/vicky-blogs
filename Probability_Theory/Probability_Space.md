# Probablity Space ( $\Omega$ , $\mathbb{A}$ , $\mathbb{P}$ )

- Sampe Space $\Omega$ : Random experiment cannot predict the outcome with certainty, e.g. coin toss , Yet we know all the possible outcomes
- The set of all possible outcomes is denoted by $\Omega$ and called **sample space** (or state space)

- An event E is said to occur on a particular trial of the experiment if the outcome observed is an element of the set E.

- Construct a sample space for the experiment that consists of tossing a single coin. The outcomes could be labeled  $h$ for heads and  $t$ for tails. Then the sample space is the set: $\Omega ={h,t}$

- Toss a coin twice $\Omega ={hh, ht, th, tt}$

- Toss a die $\Omega ={1,2,3,4,5,6}$

- Toss a die $n$ times:
    - When you toss a die $n$ times, each outcome can be represented as an ordered $n$ -tuple where each element is a number between 1 and 6 (since a die has 6 faces). The sample space is then the set of all possible such $n$ -tuples.

$$\Omega = \{(x_1, x_2, \dots, x_n) \mid x_i \in \{1, 2, 3, 4, 5, 6\} \text{ for } i = 1, 2, \dots, n\}$$
$

***

- **Empty Set ( $(\emptyset) )**: Represents an event with no possible outcomes. $(\emptyset) = 0$.
- **Union ( $A \cup B$ )**: Represents an event where either $A$, $B$, or both Poccur. $P(A \cup B)$ accounts for all outcomes in either event, correcting for overlap.
- **Intersection ( $A \cap B$ )**: Represents an event where both $A$ and $B$ occur simultaneously. $P(A \cap B)$ depends on whether the events are independent or dependent.

### De Morgan's Laws

De Morgan's laws are fundamental rules in set theory, logic, and probability theory. They describe the relationship between the complement of unions and intersections of sets. The laws are expressed as follows:

For any two sets $A$ and $B$:

1. **Complement of a Union**:
   $$\overline{A \cup B} = \overline{A} \cap \overline{B}$$
   This states that the complement of the union of two sets is equal to the intersection of their complements.

2. **Complement of an Intersection**:
   $$\overline{A \cap B} = \overline{A} \cup \overline{B}$$
   This states that the complement of the intersection of two sets is equal to the union of their complements.

### In Probability Theory

If $A$ and $B$ are events in a probability space, then De Morgan's laws can also be interpreted in terms of events:

1. **Complement of a Union**:
   $$P\left(\overline{A \cup B}\right) = P\left(\overline{A} \cap \overline{B}\right)$$

2. **Complement of an Intersection**:
   $$P\left(\overline{A \cap B}\right) = P\left(\overline{A} \cup \overline{B}\right)$$

These formulas are useful when dealing with probabilities of complements, especially when you need to simplify complex probability expressions.
