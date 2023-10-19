# Linear Regression
## Hypothesis Class
$h:x\in\mathbb R^d\rightarrow y\in\mathbb R$ 
$\mathbb H_{linear}=\{h(x):h(x)=w^Tx+b,w\in\mathbb R^d,b\in\mathbb R\}$ 

Definition for "linear function" requires the line pass the origin, since the constant term $b$ can be absorbed in the end, we call our function "linear regression".

$\tilde x=\begin{bmatrix}1\\.\\.\\.\\x\end{bmatrix}\in\mathbb R^{d+1}\qquad\tilde w=\begin{bmatrix}b\\.\\.\\.\\w\end{bmatrix}\in\mathbb R^{d+1}$ 

So far, we defined the hypothesis class.

---
## Loss Function
compare the prediction with the true value

==Mean Squared Error==: $\frac1{2M}|y^m-t^m|^2$ (same as $|\hat y^{(m)} - y^{(m)}|^2$)
- absolute error may create a corner which is no differentiable, not friendly in terms of smooths
- squared error is smoother without loss of generality

$\underset w {minimize}\quad J(w)=\frac1{2M}\sum^M_{m=1}(w^Tx^{m}-t^{(m)})^2$ 
- the $\frac12$ in the coefficient is for aesthetic purpose, since it can be canceled out when we are doing derivative (gradient).

vector form of l2 noun: $J(w)=\frac1{2M}||y-t||^2_2=\frac1{2M}||Xw-t||^2_2$
- $||v||_p=(\sum_iv_i^p)^{\frac1p}$

---
# Convex Function
we like it when we are doing optimization, because it is guarantee that we have the bottom and the process is smooth.
>[!Roadmap]
> 1. Convex Function
> 2. Optimality
> 3. Solve MES

>[!def]
># Convex Set
>A set $S$ is convex iff:
>- $\forall x,y\in S, \forall \lambda \in (0,1) \rightarrow \lambda x+(1-\lambda)y\in S$
># Convex Function
>A real-valued function $f$ is a convex function iff:
>- $Domain(f)$ is a convex set
>- $\forall x,y\in Domain(f)\qquad \forall\lambda\in(0,1)\rightarrow f(\lambda x+(1-\lambda)y)\le \lambda f(x)+(1-\lambda)f(y)$ 

Let $f$ be a twice-differentiable function defined on a convex set, then
These statements are ==equivalent==:
- $f$ is a convex function
- $(1^{st}-order)\quad\forall x,y\in Domain(f)\qquad f(y)\ge f(x)+[\nabla_x f(x)]^T(y-x)$
	- For the right-hand side of the second statement, the first term is the base height, and the second term is the derivative of the base point, that is, the trend of the linear function, times the distance between the target and the base, resulting of the height of the target in the trend of the basic linear function. 
	- Thus, the right-hand side is the linear lower bound of the convex function.
	- The second term is call an "affine function"[[#^3b3a65]]
 - $(2^{nd}-order)\quad\forall x\in Domain(f)\qquad\nabla^2_xf(x)\succeq0$
	 - Convexity
	 - $\succeq$: positive semi-definition
	 - $\nabla^2_xf(x)=\begin{pmatrix} \frac{\partial^2 f}{\partial x_1\partial x_1}&\frac{\partial^2 f}{\partial x_1\partial x_2}&...\frac{\partial^2 f}{\partial x_1\partial x_d}\\.\\.\\.\\\frac{\partial^2 f}{\partial x_d\partial x_1}\end{pmatrix}\qquad \text{Hessian matrix}$
		 - If the Hessian matrix is positive, that means every dimension is curing up.
  ---
1. affine function / transformation: a transformation that carries straight lines into straight lines and parallel lines into parallel lines but may alter distance between points and angles between lines. ^3b3a65
