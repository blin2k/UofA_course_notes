Input: $x\in\mathbb R^d$
Output: $t\in\{C_1,C_2,...,C_k\}$ discrete categories
- if k=2, that is a binary classification
- k>0, that is a multi-class classification

	The categories must be mutually exclusive. If not, that is a multi-label classification, which can be transformed to a binary classification (Y/N).

Measure of Classification
- accuracy = # correct prediction / # samples
	- may not be a good measure
		- e.g. assume the Cancer rate is 0.001. If the model output "No" for everyone, its accuracy would be 0.999. But that's not what we want.
		- the class distribution is skewed
	- need to weight different errors
		- false positive
		- false negative
		- the weights are decided by human, but humans are not omniscious 
			- not practical facing multi-classification
- precision / recall / F-measure
	- precision = # true positive / # labeled positive
		- $=\frac{TP}{TP+FP}$
	- recall = # true positive / # actual positive
		- $=\frac{TP}{TP+FN}$
	- F-measure
		- $=\frac{2\cdot P\cdot R}{P+R}$
		- ==we must recall the minority category==
			- e.g. flip the Cancer case, 0.9 is positive and 0.1 is negative
			- P=0.9
			- R=1
			- $F=\frac{2\times0.9\times1}{0.9+1}=\frac{1.8}{1.9}\approx 94.7\%$
			- that's not what we want

---
# Linear Classification

	In a d dimensional space, using a (d-1) dimensional cut to divide the space into two separated parts.

$$h(x)\begin{cases}
1\qquad w^tx+b\ge0\\
0\qquad otherwise
\end{cases}$$
Setting the prediction to be the new dimension, cases would look like this
![[Pasted image 20231102002834.png]]

---
Using linear regression model to predict a classification problem
- get a huge penalty by predicting too well
	- squash the line could work
		- but that makes the MSE too mild
			- e.g. $(0-1)^2=1$

Non-linear models can be transformed to a linear model
- manually designing non-linear features
	- set the feature in form of powers
	- $x_k=x^k$
- non-linear kernels
	- linear inner product: $<x,y>=\sum x_i\cdot y_i$
	- customized inner product: $<x,y>=...$
- learning non-linear feature mappings
	- neural networks

