# Multi-Class Classification

$target\in\{Class_1,Class_2,...,Class_k\}$

Not like simple classification where one probability comes out when another one is known, we are going to compute a score for each class.

- $z_i=w_i^Tx+b_i$
	- $i=1,...,k$
- $P_i=\frac{z_i}{\sum_j z_j}$
	- the numerator might be negative

- $\overset \sim{P_i}=exp(w_i^Tx+b_i )$
- $z=\sum \overset\sim{P_i}$
- $P_i=\frac{\overset\sim P_i}{z}=\frac{exp(w_i^Tx+b_i )}{\sum exp(w_i^Tx+b_i )}$
	- softmax
		- argmax would not leave any probability for non-max options
		- but SoftMax would

	You can use $e^{tx}$=exp(tx) instead of exp(x), where $t\in\mathbb R$. It is called ==temperature SoftMax==. The higher the temperature is, the normal the distribution is.

---
# Training

$J=-\sum^K_{i=1}t_i\cdot log(y_i)$
- $t_i$ is ==one-hot==

index representation
- $J=-log(y(t))$
	- t is an index

	The above two representations are equivalent because all those non-hot terms in the matrix representation will be 0s.

---
## Gradient of SoftMax
$\frac{\partial J}{\partial W_{i,j}}=(y_i-t_i)x_j$
$\frac{\partial J}{\partial b_{i}}=y_i-t_i$

- i -> index of classes 
- j -> index of features

---
missing something...
fetch it when available.

---
# MAP Inference
y = argmax P(t=k | x)

expected risk
- $\underset {x\sim P(x), t\sim P(t|x)}E[\mathbb 1\{h(x)\not=b\}]=E[1-\mathbb 1\{h(x)=b\}]$
	- $\mathbb 1$: indicator functions
		- Boolean
- $\Rightarrow \underset{x\sim P(x)} E[1-\sum^K_{k=1}P(t=k|x)\cdot\mathbb 1\{h(x)=t\}]$

	need more comprehension here. Review the video when available.
---
model
- parametric
	- fixed number of parameters
- non-parametric
	- number of parameters may vary
		- usually depend on the number of samples

---
regression
- logistic
	- t in {0,1}
	- $z=w^Tx+b$
		- only one class to determine true or false
	- $y=\sigma(z)=\frac1{1+e^{-z}}$
		- sigmoid turns the score into probability
		- $P(t=1|x)=y$
			- the probability of the sample with given features is in the class
	- $J^{(m)}=-t^{(m)}\cdot log(y)^{(m)}-(1-t^{(m)})\cdot log(1-y^{(m)})$
		- the loss function for the m-th sample
		- MLE
	- optimization for MLE
		- $\frac{\partial J^{(m)}}{\partial w_i}=(y^{(m)}-t^{(m)})\cdot x_i^{(m)}$
			- the error times the feature
	- MAP
		- same as MLE but
			- Gaussian prior -> l2 penalty
			- Laplacian prior -> l1 penalty
	- inference
		- $y\ge 0.5\rightarrow w^Tx+b\ge0$
			- $\hat t=1$
		- otherwise
			- $\hat t=0$
- SoftMax
	- t in {1, 2, …, k}
	- $z_k=w_k^Tx+b_k$
		- multi-class
		- the score for the k-th class
	- $\overset \sim y_k=exp(z_k)$
		- unnormalized measure for the k-th class
		- ensure the score positive
	- $Z=\sum_k\overset\sim y_k$
		- partition function
		- the total score of the current sample
	- $y_k=\frac1Z\cdot\overset\sim y_k=\frac{exp(w^T_kx+b_k)}{\sum_{k'} exp(w^T_kx+b_k)}$
		- normalize the score, so it becomes the probability
		- $P(t=k|x)=y_k$
		- for this specific sample, we have different non-zero scores for it in different classes, so as the probability 
		- $W\in\mathbb R^{k\times d}$
		- $y,b\in\mathbb R^k$
	- $J^{(m)}=-\sum^K_{k=1}t^{(m)}_k\cdot log(y^{(m)}_k)=-log(y^{(m)}_{t^{(m)}})$
		- MLE
		- $t=[\mathcal 1\{t=1\},\mathcal 1\{t=2\},...,\mathcal 1\{t=k\}]^T$
			- it is a column vector
			- indicating if the feature is applied
	- optimization for MLE
		- $\frac{\partial J^{(m)}}{\partial w_{i,j}}=(y_i^{(m)}-t_i^{(m)})\cdot x_j^{(m)}$
			- i for category
			- j for feature 
	- MAP
		- same as MLE but
			- Gaussian prior -> l2 penalty
			- Laplacian prior -> l1 penalty
	- optimality
		- not unique
		- $\frac{exp(w_1^Tx+b_1)}{exp(w_1^T+b_1)+exp(w_0^Tx+b_0)}=\frac{1}{1+e^{-((w-w')x+(b-b'))}}$
			- if $w_*,w_*',b_*,b_*'$ is a SoftMax optimum
			- then $w_*+C,w_*'+C,b_*+C',b_*'+C'$ is also an optimum for any $C,C'\in\mathbb R$
			- ==not fully comprehending...==
	- inference
		- $\hat t=\underset k {argmax}\, y_k=\underset k{argmax}\,(w_k^Tx+b_k)$
		- minimize the expected error