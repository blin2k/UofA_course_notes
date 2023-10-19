$$\begin{align}
J&=\frac1M\sum^M_{m=1}J^{(m)}\\
\nabla J(w^{(t-1)})&=\frac1M\sum^M_{m=1}\nabla J^{(m)}(w^{(t-1)})\\
\end{align}$$
since the gradient direction may not be accurate, wasting lots resources on gradient is not a wise choice. 

we'd like to shrink the size of M, that is, randomly select B samples from M as a batch. By doing this, we save test sets and time, without large loss of generality.


sampling
- w/ replacement
	- noisier b/c duplicated samples
- w/o replacement


	100 samples would be considered a large batch


epoch
- an iteration over ==all the training samples==
- batch by batch, not necessarily

$$\begin{align}
&\text{initialize w}\\
&\text{for each epoch e=1, 2, ... until satisfied}\\
&\qquad \text{for b=1, ... }\frac MB\\
&\qquad \qquad w^{(new)}\leftarrow w^{(old)}-\alpha \frac1B\sum_{m=(b-1)B+1}^{b\cdot B}\nabla J^{(m)}(w^{(old)})\\
&\text{return the last w}
\end{align}$$

1. B=M
	1. full batch
	2. good is the objective is guaranteed convex
2. 1\<B\<M
	1. mini batch
	2. approximate the full batch update
	3. somehow better than full batch
3. B=1
	1. stochastic
	2. too noisy

	somehow a small batch performs better than a large batch 
 ---

$\nabla J(w)=X^T(Xw-t)$
vs.
$\frac{\partial}{\partial w_i}J(w)\approx \frac{J(w_i+\sigma)-J(w_i-\sigma)}{2\sigma}$ for some small $\sigma$

	always use closed-form solution if it exists and is efficient / stable / etc.

