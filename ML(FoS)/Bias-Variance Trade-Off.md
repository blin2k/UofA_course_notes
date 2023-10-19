# MLE Principle
$\bar w_{MLE}=\underset w {argmax}\quad\mathcal L(w;\mathcal D)=\underset w {argmax}\quad\mathcal P(\mathcal D;w)$

---
# Unbiasedness
	If I draw my sample again and again, the expectation will converge to the true value.

$\mathbb E_{\mathcal D}[\hat w]=w$
[[Solving MSE]]

$$\begin{align}
\mathbb E_{\mathcal D}[\hat w]&=\mathbb E_{x,\epsilon}[(X^TX)^{-1}X^Tt]\\
&=\mathbb E_{x,\epsilon}[(X^TX)^{-1}X^T(Xw+\epsilon)]\\
&=\mathbb E_{x,\epsilon}[(X^TX)^{-1}X^TXw+(X^TX)^{-1}X^T\epsilon]\\
&=\mathbb E_{x,\epsilon}[(X^TX)^{-1}X^TXw]+\mathbb E_{x,\epsilon}[(X^TX)^{-1}X^T\epsilon]\\
&=\mathbb E_{x,\epsilon}[w]+\mathbb E_{x,\epsilon}[(X^TX)^{-1}X^T]\cdot\mathbb E_{x,\epsilon}[\epsilon]\\
&=w+\mathbb E_{x,\epsilon}[(X^TX)^{-1}X^T]\cdot 0\\
&=w
\end{align}$$

# Gauss-Markov Theorem
	Under certain conditions, the ordinary least squares (OLS) estimator of the coefficients of a linear regression model is the best linear unbiased estimater (BLUE).

The best linear weights are unbiased. 

--- 
# Risk 
h(x): hypothesis function t = f(x) + $\epsilon$ = real function + noise 
$$\begin{align} \mathbb E_{x,\epsilon}[(h(x)-t)^2]&=\mathbb E[(h(x)-f(x)-\epsilon)^2]\\ &=\mathbb E[(h(x)-f(x))^2]+\mathbb E[\epsilon^2]-2\cdot\mathbb E[(h(x)-f(x))\cdot \epsilon]\\ &=\mathbb E[(h(x)-f(x))^2]+\mathbb E[\epsilon^2] \end{align}$$ $\epsilon$ is zero-mean, so the third term can be ignored. However, $\epsilon^2$ is not zero-mean. The second term is an irreducible error (variance of noise). Compare with an "average" learned model ![[Pasted image 20231014223656.png]] D and D' are two different datasets, the expectation should be the same. So it can be canceled out.

$Var(x) = E( (X-E(X))^2 )$

$Risk = Variance + Bias^2 + Noise$

