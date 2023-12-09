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