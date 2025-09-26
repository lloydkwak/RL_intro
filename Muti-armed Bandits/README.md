# Goal
study the evaluative aspect of reinforcement learning in a simplified setting.

- nonassociative setting : does not invlove learning to act in more than one situation.


# k-armed Bandit Problem
- envierment : k different actions, each you receive a numerical reward.
- objective : maximize the expected total rewards over some time period.

each of the k actions has an expected or mean reward given that that action is selected.

### value of the action
$$q_* (a) \doteq \mathbb{E}[R_t | A_t=a]$$
- $A_t$ : action selected on time step $t$
- $R_t$ : corresponding reward
---
At any time step there is at least one action whose estimated value is greatest. These are called greedy actions.

- exploitation : select greedy actions

- exploration : select nongreedy action

### Goal is to balance exploration and exploitation

# Action-value Methods
Methods for estimating the value of actions and for using the estimates to make action selection decision.

Averaging the rewards actually received

$$Q_t(a) \doteq \frac{\sum_{i=1}^{t-1}R_i\cdot1_{A_i=a}}{\sum_{i=1}^{t-1}1_{A_i=a}}$$

- $1_{predicate}$ : random variable that is 1 if $predicate$ is true ans 0 if it is not

As denominator goes to infinity $Q_t(a)$ converges to $q_*(a)$.

# Incremental Implementation
Concentrate on a single action

$$Q_n\doteq \frac{R_1 + R_2 + \cdot\cdot\cdot + R_{n-1}}{n-1}$$
- $Q_n$ : the estimate of its action value after it has been selected $n-1$ times
- $R_i$ : the reward received after the $i$ th selection

If this is done, then the memory and computational requirments would grow over time.

$$Q_{n+1}
= \frac{1}{n}\sum_{i=1}^{n-1}R_i
\
= \frac{1}{n}\bigl(R_n + \sum_{i=1}^{n-1}R_i\bigr)
\
= \frac{1}{n}\Bigl(R_n + (n-1)\tfrac{1}{n-1}\sum_{i=1}^{n-1}R_i\Bigr)
\
= \frac{1}{n}\bigl(R_n + (n-1)Q_n\bigr)
\
= \frac{1}{n}\bigl(R_n + nQ_n - Q_n\bigr)
\
= Q_n + \frac{1}{n}\bigl[R_n - Q_n\bigr]$$

$$\downarrow$$
---
---
### $$NewEstimate\leftarrow OldEstmate + StepSize[Target - OldEstimate]$$
- $[Target - OldEstimate]$ if an $error$ in the estimate
- $StepSize$ changes from time step to time step

---
---
### Initialize, for a = 1 to k
- $Q(a) \leftarrow 0$
- $N(a) \leftarrow 0$

### Loop forever:
- $A \leftarrow \begin{cases}
\arg\max_a Q(a) & \text{with probability } 1-\epsilon \text{ (break ties random)} \\
\text{random action} & \text{with probability } \epsilon
\end{cases}$
- $R \leftarrow bandit(A)$ : take action $a$ and return reward
- $N(A) \leftarrow N(A) + 1$
- $Q(A) \leftarrow Q(A) + \frac{1}{N(A)}[R-Q(A)]$
---
---

