$\Omega,\epsilon,P$

$P:\epsilon\rightarrow\mathbb R$
- Non-negative
	- $\forall E\in\epsilon\qquad P(E)\ge0$
- Normalizing
	- $P(\Omega)=1$
- $\delta$-additive
	- $\forall \quad disjoint\quad E_1,E_2,...\in\epsilon\qquad P(\cup_iE_i)=\sum_iP(E_i)$

---
- Joint Probability
	- $P(X,Y)=P(Y)\cdot P(X|Y)=P(X)\cdot P(Y|X)$
	- if $X\perp Y \qquad P(X,Y)=P(X)\cdot P(Y)$
- Conditional Probability
	- $P(X|Y)=\frac{P(X,Y)}{P(Y)}$
	- if $X\perp Y\qquad P(X|Y)=P(X)$
- Marginal Probability
	- $P(X)=\sum_YP(X,Y)$
- Bayes' Rule
	- $P(X|Y)=\frac{P(X,Y)}{P(Y)}=\frac{P(X)\cdot P(Y|X)}{\sum_{x'}P(X',Y)}=\frac{P(X)\cdot P(Y|X)}{\sum_{x'}P(X')\cdot P(Y|X')}$
- Expectation
	- $\mathbb E_{X\sim P(X)}[f(x)]=\sum_xp(x)f(x)$
---
# Maximum Likelihood Estimation

Frequentist point of view:
- data are random variables
- weight is ==not==
	- it is an experience, a fact, something goes with the world and cannot restart

$$\begin{align}
&\mathcal D=\{(x^{(m)},t^{(m)})\}^M_{m=1}\\
&\text{Linear regresson: }t=w^Tx\\
&\text{Assume }t^{(m)}\sim \mathcal N(w^Tx^{(m)}, \sigma^2)\qquad\text{ for some unknown constant } w\\
&P(t^{(m)}|x^{(m)};w)=\frac1{\sqrt{2\pi}\sigma}exp\left\{-\frac12(\frac{t^{(m)}-w^Tx^{(m)}}{\sigma})^2\right\}\\
&\text{The probability of the whole dataset: }\\
&\qquad P(t^{(1)}, ...,t^{(M)}|x^{(1)},...,x^{(M)};w)\\
&=\prod^M_{m=1}P(t^{(m)}|x^{(1)},...,x^{(M)};w)\qquad\text{independent events}\\
&=\prod^M_{m=1}P(t^{(m)}|x^{(M)};w)\\
&=\prod^M_{m=1}\frac1{\sqrt{2\pi}\sigma}exp\left\{-\frac12(\frac{t^{(m)}-w^Tx^{(m)}}{\sigma})^2\right\}\\
\end{align}$$
![[Pasted image 20231012125645.png]]
In this t-x function, we aware the existence of the noise, and the distribution of the true value. Combining them means, for each data point, we know the confidence interval (vertical deviation). 

The probability space of the whole data set is the sum of all those intervals.

$\epsilon^{(m)}\sim \mathcal N(0,\sigma^2)$
$t^{(m)}\sim \mathcal N(w^Tx^{(m)},\sigma^2)$

---
## MLE
	Find the best w that makes data most likely happen.

$\bar w_{MLE}=\underset{w}{argmax}\quad P(t^{(1)},...,t^{(M)}|x^{(1)},...,x^{(M)};w)=\underset{w}{argmax}\quad P(\mathcal D;w)=\underset{w}{argmax}\quad \mathcal L(w;\mathcal D)$

	Under this weight, we have the biggest chance to get this dataset (reality).

notice that, the MLE of Normal Distribution is equivalent to argmin of MSE $J(w)$.
![[Pasted image 20231012143615.png]]
