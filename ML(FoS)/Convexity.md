This is how your loss function revolute: 
1. $J(w)=w^Tx^{(m)}-t^{(m)}$
	1. the $m^{th}$ sample: prediction - target
2. $J(w)=(w^Tx^{(m)}-t^{(m)})^2$
	1. make it smooth
3. $J(w)=\frac1{2M}\sum^M_{m=1}(w^Tx^{(m)}-t^{(m)})^2$ 
	1. get the average of all loss, and the magic number for future convenience
4.  $J(w)=\frac1{2M}\sum^M_{m=1}||Xw-t||_2^2$        (the subscript 2 indicates L2 form)
	1. $X=\begin{bmatrix}(x^{1})^T\\.\\.\\.\\(x^{M})^T\end{bmatrix}_{M\times d}\qquad w\in\mathbb R^d\qquad t=\begin{bmatrix}t^{(1)}\\.\\.\\.\\t^{(M)}\end{bmatrix}\in\mathbb R^M$
	2. vector representation
 ---
# proof (1st-order -> convex function)
## premise
$\forall x,y\qquad f(y)\ge f(x)+[\nabla f(x)]^T(y-x)$
- $1^{st}-order$
## goal
$\forall x,y\quad\forall \lambda\in(0,1)\qquad \lambda f(x)+(1-\lambda)f(y)\ge f(\lambda x+(1-\lambda)y)$
- The function is convex

## proof
Consider any $x,y\in Dom(f)\qquad$ any $\lambda\in(0,1)$
define $z=\lambda x+(1-\lambda)y$
$$\begin{align}
\because f(x)&\ge f(z)+[\nabla f(z)]^T(x-z)\\
f(y)&\ge f(z)+[\nabla f(z)]^T(y-z)\\
\therefore \lambda \cdot f(x)+(1-\lambda)\cdot f(y)&\ge (\lambda+1-\lambda)f(z)+ [\nabla f(z)]^T[\lambda(x-z)+(1-\lambda)(y-z)]\\
&=f(z)+[\nabla f(z)]^T[\lambda x+(1-\lambda)y-z]\\
\because z&=\lambda x+(1-\lambda)y\\
\therefore \lambda f(x)+(1-\lambda)f(y)&\ge f(z)+0\\
\rightarrow \lambda f(x)+(1-\lambda)f(y)&\ge f(\lambda x+(1-\lambda)y)\qquad\square
\end{align}$$
---
# proof (2nd-order -> 1st-order)

$\forall x,y\in Dom(f)\qquad f(y)=f(x)+[\nabla f(x)]^T(y-x)+\frac12(y-x)^T\nabla_x^2f(\xi)(y-x)$
- This is a linear approximation (Taylor expansion), thus the equal sign is not correct since the distance between x and y could be very long
- Need to solve for some $\xi$ between $x$ and $y$, because by Lagrange's Mean Value Theorem, there must exist a point between x and y, where the slope equals the slope of the line passing x and y

By the 2nd-order condition, $\nabla_x^2f(\xi)\succeq0$, therefore the second term will be greater or equal to 0  (scalar)

Because the second term is positive, we can conclude that $f(y)\ge f(x)+[\nabla f(x)]^T(y-x)\qquad\square$

---
# proof (the convexity of MSE)
$$\begin{align}J(w)&=\frac1{2M}\sum^M_{m=1}(w^Tx^{m}-t^{(m)})^2\\
&=\frac1{2M}||Xw-t||^2_2
\end{align}$$

	The subscript 2 indicates L2 form