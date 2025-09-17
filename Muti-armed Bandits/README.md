# Goal
study the evaluative aspect of reinforcement learning in a simplified setting.

- nonassociative setting : does not invlove learning to act in more than one situation.


# k-armed Bandit Problem
- envierment : k different actions, each you receive a numerical reward.
- objective : maximize the expected total rewards over some time period.

each of the k actions has an expected or mean reward given that that action is selected.

### value of the action
$$q_* (a) \doteq \mathbb{E}[R_t | A_t=a]$$
- $A_T$ : action selected on time step $t$
- $R_t$ : corresponding reward
---
At any time step there is at least one action whose estimated value is greatest. These are called greedy actions.

- exploitation : select greedy actions

- exploration : select nongreedy action

### Goal is to balance exploration and exploitation