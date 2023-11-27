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
		- but softmax would
