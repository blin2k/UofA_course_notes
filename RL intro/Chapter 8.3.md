# Model

- TD learns from the experience
	- could be expensive to experience again and again
- DP learns from how things work
	- could be expensive to retrieve the function

It would be good if we can leverage these two.

A model
- creates
	- simulated experience
- updates
	- value function
- modifies
	- policy

	A model is a simulated environment based on incomplete knowledge. 

## Types of Model

- Sample Model
	- simulates the exact outcome
		- e.g. head or tail from coin flipping
	- inexpensive
		- produce single output multiple time
	- require less memory
- Distribution Model
	- specifies the likelihood or probability
	- more information
		- can be used directly
		- compute the exact expected outcome
	- difficult to specify
		- need to consider the joint situation
	- assess risk

---
# Planning

	Planning takes a model as input, and ouput an improved policy.

- Q-learning 
	- updates the policy from the environment,
- Q-planning
	- updates the policy from the model. 

## Random-sample One-step Tabular Q-planning

Assuming we have the state-action pair, the model outputs the next state and the reward according to the input pair.

Then we can apply Q-learning to update the value function. Using a greedy policy improvement, the policy is improved.

- planning ==only== uses imagined experience
- the agent can do this without behaving in the real world
	- or keep planning and behaving in parallel
---
# Dyna Architecture

In Q-learning, at the end of the first episode, the agent only updates the action-value function for the state before termination. 

The Q-planning takes advantage of the experience from that episode. The agent may not explore all states at the first episode, but for all explored states, we can update the related action-value function.
- with Q-planning, the agent knows how to get to the destination immediately after the first episode
	- a greedy agent would stick on this solution
	- but the strategy is not likely optimal because it only learned once

## Tabular Dyna-Q

1. initialize Q(s, a) and Model(s, a)
2. LOOP forever
	1. S <- current state
	2. A <- e-greedy(s, a)
	3. take action A and observe resultant reward R and state S'
	4. $Q(S,A)\leftarrow Q(S,A)+\alpha[R+\gamma\cdot {max}_aQ(S',a)-Q(S,A)]$
	5. Model(S, A) <- R, S'
	6. LOOP n times
		1. S <- random previous observed state
		2. A <- random action previously taken in S
		3. R, S' <- Model(S, A)
		4. $Q(S,A)\leftarrow Q(S,A)+\alpha[R+\gamma\cdot {max}_aQ(S',a)-Q(S,A)]$

- search control
	- random
	- previous observed
- model query
	- the simulation of what would happen if we move to the next state in the model
- value update

If the model was correct, more planning leads to faster learning.
- 6 planning updates is good enough
	- too many planning would waste lots of time at beginning because of the randomness

---
## Inaccurate Model

- incomplete model
	- don't know the resultant for the chosen state
	- can be solved by exploration and search control
- changing environment
	- same (s, a) leads to a different (r, s') from previous observation
	- can be improved by check the outcome again (a different kind of exploration)
		- $r+\kappa\sqrt{\tau}$
			- $\tau$: time steps since transition was last tried
			- $\kappa:$ small constant

Adding this new reward bonus to Dyna-Q's planning updates results in the ==Dyna-Q+== algorithm

