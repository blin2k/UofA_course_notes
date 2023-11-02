# Sigmoid

We know that the hypothesis function looks like a ladder because of the output can only be 0 and 1
- h(x) is not differentiable, thus gradient descent cannot be applied
- to reduce the inconvenience, we need a ==smooth squashing function== instead of the step function above
	- ==sigmoid function==
		- $\sigma(z)=\frac1{1+e^{-z}}$
			- $z=w^Tx+b$
			- ==need to be memorized==, will be tested in the final
			- $\sigma(0)=\frac12$
			- $\sigma(\infty)=1$
			- $\sigma(-\infty)=0$
			- $\sigma(z)=1-\sigma(-z)$
		- it is not the only function acts in that way (e.g. probit function), but it is easy to compute

## Summary
- $y=\sigma(w^Tx+b)=\frac1{1+e^{-(w^Tx+b)}}$
- $\hat t=h(x)$
	- 0 if $y\ge\frac12$
	- 1 otherwise

Applying MSE to y and t may not work either
- too mild if the prediction is wrong