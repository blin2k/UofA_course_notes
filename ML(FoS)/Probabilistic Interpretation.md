# Probability

Interpretation
- Frequentists
	- count the fraction of occurrences in ==repeatable== experiment
	- e.g. flip a coin
- Bayesian
	- subjective belief
	- e.g. weather

 > [!notice]
 > # Science is subjective.
 > why?
 > Confidence Interval
 > No way to prove that math is consistant

---
# Kolmogorov Axiom

- sample space $\Omega$
	- atomic events
- event space $\epsilon$
	- $E\in\epsilon, E\in \mathcal P(\Omega)$
		- discrete case: 
			- $\epsilon$ can be $\mathcal P(\Omega)$           (power set: empty + combinations + full)
		- continuous case: 
			- $\mathcal P(\Omega)$ consists of intervals
			- single event has zero probability
	- $\emptyset,\Omega\in\epsilon$
- $P:\epsilon\rightarrow\mathbb R$
	- non negative
		- $\forall E\in\epsilon,P(E)\ge0$
	- normalized
		- $P(\Omega)=1$
	- additive
		- $\forall \text{ disjoint }E_1,E_2,...\in\epsilon\rightarrow P(\cup_iE_i)=\sum_iP(E_i)$


	Continuum Hypothesis: $|\mathbb N| < ? < |\mathbb R|$

---
## Joint Probability
- $P(X,Y)=P(X)\cdot P(Y|X)=P(Y)\cdot P(X|Y)$

## Conditional Probability
- $P(Y|X)=\frac{P(X,Y)}{P(X)}$

## Marginal Probability
- $P(X)=\sum_YP(X,Y)$

## Bayes' Rule
- $P(X|Y)=\frac{P(X,Y)}{P(Y)}=\frac{P(X)\cdot P(Y|X)}{\sum_{X'}P(X')\cdot P(Y|X')}$
for continuous cases, the summation would be integral.

## Expectation
- $\mathbb E[f(X)]=\sum_XP(X)f(X)=\int P(X)f(X)dx$