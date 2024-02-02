# Absolut and Relative Errors
- absolute error
	- approximate value - true value
- relative error
	- (absolute error)/(true value)

# Data and Computational Errors
- propagated data error
	- $f(\hat x)-f(x)$
	- working with inexact inputs
- computational error
	- $\hat f(\hat x)-f(\hat x)$
	- function approximation
- total error
	- the sum of these two errors
- truncation error
	- terminating an iterative process before it converges or by using a limited number of terms in an infinite series
- rounding error
	- limited-precision

# Forward and Backward Errors
- forward error
	- $\Delta y=\hat y-y$
	- using the same input, the difference in the outputs
- backward error
	- $\Delta x=\hat x-x$
	- $\hat y=\hat f(x)=f(\hat x)$
	- to get the same output, the difference in the inputs
- ![[Pasted image 20240129180112.png]]

If $\Delta x/x$ is small, then $f(\hat x)$ is a near problem
- because the backward error is small

# Sensitivity and Conditioning
- insensitive == well-conditioned
	- relative change in input causes a similar degree of relative change in output
- sensitive == ill-conditioned
	- opposite
- condition number
	- $\frac{\Delta y/y}{\Delta x/x}$
	- based on relative forward and backward errors
	- if the condition number much larger than 1, we are dealing with ill-conditioning
	- $\approx\frac{x\cdot f'(x)}{f(x)}$

# Computer Arithmetic
- infinite continuum of real numbers is approximated by ==finite and discrete floating-point number systems==
	- the finite precision of floating-point arithmetic results in numerical problems such as inaccuracy, overflow, underflow, and cancellation

# Floating-Point Representation of Numbers
- $1984=1,984\times10^3=(1+\frac9{10}+\frac8{10^2}+\frac4{10^3})\times10^3$
- $\pm(d_0+\frac{d_1}{\beta}+\frac{d_2}{\beta^2}+...+\frac{d_{p-1}}{\beta^{p-1}})\times\beta^E$
	- base $\beta$
	- precision p
	- exponent E

# Normalization
- the leading digit $d_0$ is always non-zero except when the number representing is zero
- machine numbers
	- $2(\beta-1)\beta^{p-1}(U-L+1)+1$
		- binary system with p=3, $E\in[-1,1]$ 
		- can represent $2*1*2^2*3+1=25$ machine numbers

# Overflow and Underflow
- the largest floating-point number
	- overflow level (OFL)
	- $\beta^{U+1}(a-\beta^{-p})$
- the smallest
	- underflow level (UFL)
	- $\beta^L$

# Rounding Rules
- chop or round toward zero
	- the base-$\beta$ expansion is truncated after (p-1)st digit
- round to nearest/even
![[Pasted image 20240129182941.png]]
# Machine Precision
- $|\frac{fl(x)-x}{x}|\le\epsilon_{mach}$
	- the accuracy of a floating-point system is bounded by machine precision $\epsilon_{mach}$
	- $fl(1+\epsilon)>1$
	- $0<UFL<\epsilon<OFL$
- chopping
	- $\beta^{1-p}$
- even
	- $0.5\times\beta^{1-p}$

# Cancellation
In rounding errors, we lose the least significant digits, whereas in cancellation we lose the most significant digits.
- $fl(1+\epsilon)-fl(1-\epsilon)=1-1=0$
- $fl(1+\epsilon-(1-\epsilon))=2\epsilon$