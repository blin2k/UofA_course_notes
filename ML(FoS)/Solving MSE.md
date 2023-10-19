$$
\begin{align}
\nabla J(\omega)=\frac1MX^T(X\omega-t)&\overset{set}=0\\
X^TX\omega-X^Tt&=0\\
\omega&=(X^TX)^{-1}X^Tt\qquad\text{if }X^TX\text{ is invertible: }det()\not=0 \\
\end{align}
$$
1. d > M
	1. small sample size
		1. large portion of the sample could be outliers
		2. model won't work well
	3. $rank(X^TX)\le min(d,M)$
		1. empty entries
		2. not invertible
$$
\text{feature selection}\begin{cases}
\text{prior knowledge}\\
\text{stat correlation}\\
\text{integrated into ML model space model}
\end{cases}
$$
2. $d\le M$ but you have duplicate features
	1. rows could be canceled out, thus the rank of the matrix is not full
		1. $rank(X^TX)<min(d,M)$
			1. not invertible

Noticing that, the 2nd case doesn't hurt the ML model
$\omega=(X^TX)^\dagger X^Tt$

	the symbol $\dagger$ (dagger) represents "pseudo inverse "

applying pseudo inverse to the 1st case does not give runtime error, but it does not work in practice either

---
# Drawback of Closed Form Solution

- $()^{-1}$ is expensive and not stable
	- the result might overflow
	- in $O(d^3)$
		- slow and inefficient
  
  ---
# Gradient Descent 

- initial $w^{(0)}$
	- randomly / all zeros
		- doesn't matter for convex optimization
		- all 0s is bad for non-convex function
			- loss function has symmetry
- for t=1, t++, until satisfied
	- $w^{(t)}\leftarrow w^{(t-1)}-\alpha \nabla J(w^{(t-1)})$


- how many iteration?
	- budget
	- until converge
		- $||w^{(t-1)}-w^{(t)}||$
			- bad
			- large or not depends on the sensitivity of the task
		- $|J_{D_{hold}}(w^{(t-1)})-J_{D_{hold}}(w^{(t)})|$
			- good
		- $|Err_{D_{hold}}(w^{(t-1)})-Err_{D_{hold}}(w^{(t)})|$
			- the best
- how to choose $\alpha$
	- too large
		- overshooting
	- too small
		- slow
	- adaptive
		- large $\rightarrow$ small
	- adaptive for each weight
		- modern development
---
# GD May Lead to a Inefficient Direction:

think about Lili's salad bowl. GD would always tell you to go along with the tangent line, in which way you will probably reach the bottom after tons of iterations.

however, the shortest path is the line connecting where you are and the bottom. in other words, your track is a curve line instead of a straight line.

therefore, we don't have to take it too serious. we only need a sample of the training set to calculate the gradient