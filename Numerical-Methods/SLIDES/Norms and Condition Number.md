	We define the norm of a vector as the sum of p powers under p roots.

p-norms
- $||x||_p=(\sum^n_{i=1}|x_i|^p)^{1/p}$
- $||x||_\infty=max_i|x_i|$

for any vector
- $||x||_1\ge||x||_2\ge||x||_\infty$
- $||x||_1\le\sqrt n\cdot||x||_2$
- $||x||_2\le\sqrt n\cdot||x||_\infty$
- $||x||_1\le n\cdot||x||_\infty$

# Properties
- $x\not=0\rightarrow||x||>0$
- $||\gamma x||=|\gamma|\cdot||x||$ for any scalar $\gamma$
- $||x+y||\le||x||+||y||$
	- triangle inequality
	- $|\,||x||-||y||\,|\le||x-y||$

# Matrix Norms
$||A||=max_{x\not=0}\frac{||Ax||}{||x||}$
- measures maximum relative stretching matrix does to any vector in given vector norm

1-norm is maximum absolute column sum
- the largest column
inf-norm is maximum absolute row sum
- the largest row

## Properties
- $A\not=0\rightarrow||A||>0$
- $||\gamma A||=|\gamma|\cdot||A||$ for scalar $\gamma$
- $||A+B||\le||A||+||B||$
	- triangle inequality
- $||AB||\le||A||\cdot||B||$
	- sub-multiplicative
- $||Ax||\le||A||\cdot||x||$ for vector x

==Outer multiplication and addition are greater than inner.==

# Condition Number
	A reliable estimate of closeness to singularity.

$cond(A)=||A||\cdot||A^{-1}||$
- if A is singular, $cond(A)=\infty$
- stretching divided by shrinking
	- condition number measures ==ratio of maximum stretching to maximum shrinking matrix does to any nonzero vectors==
- the larger CN it has, the more it near singular
	- don't forget singular means parallel
	- ![[Pasted image 20240225003458.png]]
	- when the two vectors are getting similar, the CN increases

## Properties
- $cond(A)\ge1$
- $cond(I)=1$
- $cond(\gamma A)=cond(A)$
	- CN in some way represents the angle so the length doesn't matter
- for diagonal matrix $D=diag(d_i)$, $cond(D)=\frac{max|d_i|}{min|d_i|}$

# Computation
Matrix inverse is expensive while matrix norm is easily computed as maximum absolute column sum or row sum.

$Az=y\rightarrow \frac{||z||}{||y||}\le|A^{-1}||$
- heuristically picking y with large ratio z/y yields good estimate for $||A^{-1}||$

CN of $f(A)=Ax=b$
- $\frac{||\Delta b||/||b||}{||\Delta A||/||A||}$
- output / input

CN of $x=g(b)=A^{-1}b$
- $\frac{||\Delta x||/||x||}{||\Delta b||/||b||}$
- CN of the solution function

# Error Bounds
CN yields error bound for approximate solution to linear system.

$Ax=b$
$A\hat x=b+\Delta b$
- approximate solution and error
- $\Delta x=\hat x-x$
	- $b+\Delta b=A\hat x=A(x+\Delta x)=Ax+A\Delta x$
	- ![[Pasted image 20240225131456.png]]
	- ![[Pasted image 20240225131523.png]]
	- we got the bound for ==relative change in x==
- ![[Pasted image 20240225150212.png]]
	- relative change in estimate x due to relative change in estimate matrix A

# Residual
$r=b-A\hat x$
- residual vector of approximate solution x hat to linear system Ax=b
- $A\hat x=b-r$
- ![[Pasted image 20240225153319.png]]