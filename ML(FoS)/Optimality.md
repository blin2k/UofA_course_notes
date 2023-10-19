# Design Matrix

$x^{(i)}=\begin{pmatrix}x_{i1}\\.\\.\\.\\x_{id}\end{pmatrix}:\quad d\times1$ (the ith $x$ stands for ==the whole variable set of one single sample==)
	we can call it a vector since it is a single column

$X=\begin{pmatrix}[x^{(1)}]^T\\.\\.\\.\\ [x^{(M)}]^T\end{pmatrix}:\quad M\times d$ (each row stands for a variable set of a sample, thus, the matrix stands for a ==sample set==)

$X\cdot\omega=\begin{pmatrix}\omega_1 x_{11}+\omega_2 x_{12}+...+\omega_d x_{1d}\\.\\.\\.\\\omega_1 x_{n1}+\omega_2 x_{n2}+...+\omega_d x_{nd}\end{pmatrix}$ 

---
# Partial Derivative Approach
We know that: $\frac{\partial}{\partial\omega}J(w)=\frac1MX^T(X\omega-t)$ 

and
$$
\begin{align}
J(w)&=\frac1{2M}||X\omega-t||^2\\
&=\frac1{2M}(X\omega-t)^T(X\omega-t)\\
&=\frac1{2M}(\omega^TX^T-t^T)(X\omega-t)\\
&=\frac1{2M}(\omega^TX^TX\omega-\omega^TX^Tt-t^TX\omega+t^Tt)\\
&=\frac1{2M}(\omega^TX^TX\omega-2t^TX\omega+t^Tt)\qquad \text{because }(\omega^TX^Tt)^T=t^TX\omega\in\mathbb R\\
\end{align}
$$

>[!hint]
>- If $S$ is a symmetric matrix, then $\frac{\partial}{\partial X}X^TSX=2SX$
>	- same as $(kx^2)'=2kx$
>- $\frac\partial{\partial X}AX=A^T$
>	- same as $(kx)'=k$

thus
$$
\begin{align}
\frac\partial{\partial \omega}J(\omega)&=\frac1{2M}(2X^TX\omega-(2t^TX)^T)\\
&=\frac1{2M}(2X^TX\omega-2X^Tt)\\
&=\frac{1}{M}(X^TX\omega-X^Tt)\\
&=\frac{1}{M}X^T(X\omega-t)\\
\end{align}
$$
which is the same as the result we got before. 

>[!hint]
>A symmetric matrix $S$ is P.S.D iff:
>for every vector $v\qquad v^TSv\le0$

then, $\nabla^2_\omega J(\omega)=\frac1MX^TX\succeq0$

and thus, ==MSE is a convex loss.==

---
## For convex functions, ==local optimum $\Rightarrow$ global optimum==

>[! definition]
># local optimum
> $x\in dom(f)$ is a local optimum iff: 
>	there exists $\epsilon >0$ for every point $y\in dom(f)$
>	$|y-x|<\epsilon\rightarrow f(x)\le f(y)$
># global optimum
> $x\in dom(f)$ is a global optimum iff: 
>	for every point $y\in dom(f)$
>	$f(x)\le f(y)$

	global optimum may not be unique.

### proof

Consider any point $y\in dom(f)$, 
- if $|y-x|<\epsilon\rightarrow f(y)\ge f(x)$
- if $|y-x|>\epsilon$:
	- consider a point $z=\lambda x+(1-\lambda)y$, and $|x,z|=\frac\epsilon2$
	- the solution is $\lambda = \frac{|y-x|-\frac\epsilon2}{|y-x|}\in(0,1)$
		- convexity asserts that $f(z)\le \lambda f(x)+(1-\lambda)f(y)$ 
		- locally optimality asserts that $f(x)\le f(z)$
	- $\rightarrow f(x)\le\lambda f(x)+(1-\lambda)f(y)$
	- $\rightarrow f(x)\le f(y)$

 >[!notice]
 >$\nabla f(x)=0\rightarrow \text{x is a local/global optimum}$
 >$\nabla f(x)=0\not\leftarrow \text{x is a local/global optimum}$
 