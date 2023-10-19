# Trade-off Between Bias and Variance
![[Pasted image 20231018191936.png]]

When the model is less complex than the real case, your model may fits the training data and have low variance, but it actually has high bias and thus will not perform well on the test data.

If the complexity of the model is close to the real case, your model may not fits the training data well and have high variance, however, it actually has low bias and thus will perform well on the test data.

Our design should be the intersection point of complexity and performance.

	Deep Learning is low biased AND low variance

Increasing sample size could decrease the variance of your model.

---
- select a subset of features
	- pro: reduce variance
	- con: the entire feature is gone
- keep all features, but still tune the power of Hypothesis Class $\mathcal H$
	- idea: restrict the magnitude of w
		- $\mathcal H_2=\{h(x)=w^Tx:\quad w\in\mathbb R^{d+1},||w||_2<C\}$
$$\begin{align}
\text{Training objective:}\\
&\underset w {minimize}\quad\frac1{2M}||Xw-t||^2\\
&\text{subject to } ||w||^2_2<C\\
\\
&\Updownarrow\text{Slater's condition}\\
\\
&\underset w {minimize}\quad \frac1{2M}||Xw-t||^2+\lambda\cdot||w||^2_2\qquad\text{for some }\lambda\ge0

\end{align}
$$
	$\lambda$ and C cannot be learned by ML system, they are hyper-parameters
 
---
## $l_1$-penalty

$$\begin{align}
\text{Training objective:}\\
&\underset w {minimize}\quad\frac1{2M}||Xw-t||^2\\
&\text{subject to } ||w||_1<C\\
\\
&\Updownarrow\text{Slater's condition}\\
\\
&\underset w {minimize}\quad \frac1{2M}||Xw-t||^2+\lambda\cdot||w||_{1}    \qquad\text{for some }\lambda

\end{align}
$$
![[Pasted image 20231018212248.png]]

Most of the case, with $l_1-penalty$, the closest point to the optimal would be the tip of the diamond. That means, some or most weights will be 0s. In the 2D example, $w=(x,y)$, and we can see that the closest point is some $(0,y')$.

On the other hand, with $l_2-penalty$, most weights will not be 0s.

- Many features, few samples -> sparse model -> $l_1$
- Many samples, few features -> non-sparse model -> $l_2$

Feasible set
- $l_1-penalty$
	- square / diamond
		- because $l_1$ norm $||w||_1=\sum |w|$, same idea as $|y|+|x|\le C$ 
- $l_2-penalty$
	- circle / sphere
		- $l_2:\quad ||w||_2=\sqrt{\sum w^2}$, same idea as $y^2+x^2\le C^2$

