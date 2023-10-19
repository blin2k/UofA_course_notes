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
		- 