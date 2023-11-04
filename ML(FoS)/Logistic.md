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
	- soft prediction
- $\hat t=h(x)$
	- 0 if $y\ge\frac12$
	- 1 otherwise

Applying MSE to y and t may not work either
- too mild if the prediction is wrong

---
# Probabilistic Interpretation

Bernoulli Distribution
- $t\in\{0,1\}$
- $t\sim Bernoulli(\pi)$
	- $\pi\in[0,1]$
- $Pr(t=1)=\pi$
- $Pr(t=0)=1-\pi$

# Cross-Entry Loss

In linear regression, the true value is normally distributed around the predicted value
- $t^{(m)}\sim \mathcal N(w^Tx,\sigma_\epsilon^2)$

Here, we have
- $t^{(m)}\sim Bernoulli(\pi^{(m)})$
	- $\pi^{(m)}=y^{(m)}$
		- sigmoid
- $\mathcal L=\prod^M_{m=1}(y^{(m)})^{t^{(m)}}\cdot(1-y^{(m)})^{1-t^{(m)}}$
	- only the term where $t^{(m)}=1$ will left
		- $y^{(m)}$
		- or $1-y^{(m)}$

$$\begin{align}
\underset{w,b}{maximize} \quad\mathcal L
&\Leftrightarrow
\underset{w,b}{maximize} \quad ln(\mathcal L)\\
&\Leftrightarrow
\underset{w,b}{maximize} \quad ln(\prod y^{(m)})\\
&\Leftrightarrow
\underset{w,b}{maximize} \quad \sum ln(y^{(m)})\\
&\Leftrightarrow
\underset{w,b}{minimize} \quad \sum -ln(y^{(m)})\\
&\Leftrightarrow
\underset{w,b}{minimize} \quad \sum ln({1+e^{-(w^Tx+b)}})\\
&\text{or the equivalent}\\
\text{the completed form is }\\
&\underset{w,b}{minimize} \quad \sum -t^{(m)}\cdot ln(y^{(m)})-(1-t^{(m)})\cdot ln(1-y^{(m)})
\end{align}$$

Applying partial derivative
- $\nabla_w J=\frac{\nabla_z J}{\nabla_w z}$
	- $\nabla_z J^{(m)}=y^{(m)}-t^{(m)}\in(-1,1)$
	- $\nabla_w J^{(m)}=\sum (y^{(m)}-t^{(m)})\cdot x^{(m)}$
