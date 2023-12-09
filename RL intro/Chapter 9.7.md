# Coarse Coding

Recall linear value function approximation
- $v_\pi(s)\approx \hat v(s,w)=w^Tx(s)$
	- train a linear model to learn the approximate value for the state
	- the feature is depend on the specific state

tabular
- implement by using a one-hot vector to indicate which is the current state
- not perfect when the number of states is large
	- need too many memories

aggregation
- divide the states into several parts and treat them the same
	- saving memories
- the shape of each part can be different
	- as long as one state maps to and only maps to one part
 
coarse coding
- special aggregation where one state can maps to several parts
	- overlapping on graphical representation
- more flexible class and feature choosing
- the feature vector is not one-hot anymore

# Tile Coding
	A specific type of coarse coding.
- performs an exhaustive partition of the state space using overlapping grids
- use square as the shape of an aggregated area
	- easy to implement in grid representation
	- larger tiles will result in increased generalization
- in order to have discrimination [[Chapter 9.4#Generalization and Discrimination]]
	- put several tiling (grid) on top of each other
	- ![[Pasted image 20231206111046.png]]
	- in each tiling, the updated tile is not completely the same
- direction of generalization
	- using rectangles instead of squares
	- as the dimension increases, we need more tiling

## Tile Coding in TD 
![[Pasted image 20231206155518.png]]

![[Pasted image 20231206155718.png]]
In the state aggregation, each interval is sized in 200 units.

In the tile coding, the interval is also 200 units but we have 6 tiles instead of 5 in each tiling. In this way, one tiling can still cover all the states after shifting.

Additionally, we have 50 tiling, which is also the length of the feature vector.

==Tile coding converge faster than state aggregation.==

---
# Neural Network
	Non-linear function approximation

When new data comes into the input layer, it will fit one ore more nodes. The current layer will do some computation and then send the result to the next layer through the connection between nodes. 
- feed forward neural network
- none of the connections go back
	- if they did, the output could influence its own input
	- recurrent neural network

If a node receive multiple inputs from the previous layer, the current node should sum them up with weights, then put the sum as an input of its activation function.
- activation function
	- non-linear transformation
		- sigmoidal function
			- tanh(x)
			- logistic function
			- rectified linear units (ReLU)
			- thresholding units
- ![[Pasted image 20231206165737.png]]

Tile coding create a fixed set of features for a prediction.
Neural networks provide a strategy for learning a useful set of features.
- initial weights are important
	- we could assume it from a Normal distribution in examples
- the result of a layer is a new representation or say new feature
	- the result of same input with different weight and activation function
	- tile coding implement the same idea
		- giving new representation to describe the state

# Deep Neural Networks
The depth of the network is defined by the number of hidden layers in the network. 

In theory, a neural network need not to be deep. 
- A neural network with a single hidden layer can approximate any continuous function given that is sufficiently ==wide==
	- universal approximation property
- however, practical experience and theory suggests that deep neural networks may make it easier to approximate complex functions
	- depth allows composition of features
		- ![[Pasted image 20231206172659.png]]
	- levels of abstraction
		- each level is the composition of may layers of low-level abstractions
		- they continuously contribute to the successive layers

# Gradient Descent for Training Neural Networks

- input layer
	- s
	- weights
		- A
- middle layer
	- x
	- weights
		- B
- output layer
	- $\hat y$
$$\begin{align}
\frac{\partial}{\partial B_{jk}}L(\hat y_k,y_k)&=\frac{\partial L(\hat y_k,y_k)}{\partial \hat y_k}\cdot\frac{\partial \hat y_k}{\partial B_{jk}}\\
&=\frac{\partial L(\hat y_k,y_k)}{\partial \hat y_k}\cdot\frac{\partial \hat y_k}{\partial \theta_k}\cdot\frac{\partial\theta_k}{\partial B_{jk}}\\
&=\frac{\partial L(\hat y_k,y_k)}{\partial \hat y_k}\cdot\frac{f_B(\theta_k)}{\partial \theta_k}\cdot x_j\\
&=\delta_k^Bx_j
\\
\\
\delta_k^B&\dot=\frac{\partial L(\hat y_k,y_k)}{\partial \hat y_k}\cdot\frac{f_B(\theta_k)}{\partial \theta_k}\\
\psi&\dot=sA\\
x&\dot=f_A(\psi)\\
\theta&\dot=xB\\
\hat y&\dot=f_B(\theta )\\
\end{align}$$
![[Pasted image 20231206210249.png]]
![[Pasted image 20231206210359.png]]

Then both of them will be a delta times its input.

## The Backprop Algorithm
![[Pasted image 20231206210706.png]]
	Noticing that the computation of $\delta^A_j$ including the value of $\delta_k^B$ which is done before. This is the main idea behind Back Propagation.
	- kind similar to dynamic programming which recursively solve problems

![[Pasted image 20231206211440.png]]

## Optimization Strategies for NNs

- weight initialization
	- $w_{init}\sim\frac{\mathcal N(0,1)}{\sqrt{n_{input}}}$
- update momentum
	- $w_{t+1}\leftarrow w_t-\alpha\nabla_wL(w_t)+\lambda M_t$
	- $M_{t+1}\leftarrow \lambda M_t-\alpha\nabla_w L$
		- momentum
		- if recent gradients have all been in similar directions, then we gained momentum in that direction
- vector step sizes
	- not using global one