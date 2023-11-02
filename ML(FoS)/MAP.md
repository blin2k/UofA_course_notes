small H
- more bias
- less variance
- more likely underfitting

large H
- less bias
- more variance
- more likely overfitting

$MLE\sim MSE$
$MAP\sim Regularization$

---
# Maximize a Posteriori Estimation 

	"A posteriori" is from Latin "ā posteriōrī", which means literally, "from what is later." It describes "knowledge based solely on experience or personal observation".

Frequentist
- $\mathcal D$ is known, but is a RV
- $w$ is unknown, but is a constant
	- parameter

Bayesian
- whatever unknow is a RV
	- the probability of the RV is a ==subjective belief==

---

- prior distribution
	- $P(w)$
	- the subject belief without any information
	- e.g. $w\sim\mathcal N(0,\sigma_w^2)$
- likelihood
	- $P(\mathcal D|w)$
	- the probability of having this data set with the given weights
- posterior distribution
	- $P(w|\mathcal D)$
		- $=\frac{P(\mathcal D|w)\cdot P(w)}{P(\mathcal D)}$
		- $\propto P(\mathcal D|w)\cdot P(w)$
			- because $P(\mathcal D)=\int P(w)\cdot P(\mathcal D|w)$ is a constant in terms of $w$ (not including $w$), we can get rid of it
	- the subject belief after seeing evidence

	e.g. You go to a casino where you believe the win rate of a game is 50-50 (prior distribution). Then you have 100 games and lose 90 of them (likelihood). That makes you consider the casino is cheating, and the win rate is about 1-9 or 2-8 (posterior distribution).

---
## Principle
Estimate the best $w$

$$\begin{align}
\hat w_{MAP}&=\underset w {argmax}\quad P(w|\mathcal D)\\
&= \underset w {argmax}\quad P(w)\cdot P(\mathcal D|w) \qquad\text{Prior * Likelihood}
\end{align}
$$
	Providing the prior and the likelihood, choose the $w$ that maximize the posterior

## Example

$w\sim \mathcal N(0,\sigma^2_w)$
$(t|x,w)\sim \mathcal N(w^Tx,\sigma^2_\epsilon)$

$$\begin{align}
\hat w&=\underset w {argmax}\quad P(w)\cdot P(\mathcal D|w)\\
&=\underset w {argmax}\quad ln(P(w))+ln(P(D|w))\\
&=\underset w {argmax}\quad ln(\prod^d_{i=1}\frac1{\sqrt{2\pi}\cdot\sigma_w}\cdot exp\{-\frac {w_i^2}{2\sigma_w^2}\})\\ 
&+ ln(\prod^M_{m=1}\frac1{\sqrt{2\pi}\cdot\sigma_\epsilon}\cdot exp\{-\frac {(t^{(m)}-w^Tx^{(m)})^2}{2\sigma_\epsilon^2}\})\\
&=\underset w {argmax}\quad \sum (-\frac{w_i^2}{2\sigma^2_w})
+\sum (-\frac1{2\sigma_\epsilon^2}\cdot(t^{(m)}-w^tx^{(m)})^2)\\
&=\underset w {argmin}\quad \frac1{2M}\sum (t^{(m)}-w^Tx^{(m)})^2
+\lambda\sum w_i^2\qquad \Leftrightarrow l_2-penalized
\end{align}
$$