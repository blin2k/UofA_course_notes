### Geometric Series
- $\sum^{n-1}_{i=0}av^i=a\frac{1-v^n}{1-v}$
- usually, $0<v<1$
	- $|v|<1\rightarrow lim_{n\rightarrow\infty}v^n=0$
	- $\sum^\infty_{i=0}av^i=a\frac 1{1-v}$

### Arithmetic Series
- $\sum^{n-1}_{i=0}a+id=an+\frac{n(n-1)}2\cdot d$ 
- if $a=1$ and $d=1$, then $\sum^n_{i=1}i=\frac{n(n+1)}2$

---
### Mix Type
 An annuity is a sequence of payments. 
	If the payments are constant, the annuity is called a level annuity.

$A=Pv+(P+Q)v^2+(P+2Q)v^3+(P+3Q)v^4+...+(P+(n-1)Q)v^n$
- $v=\frac 1 {1+i} \rightarrow i=\frac{1-v}v$

1. $\frac A v=P+(P+Q)v+...+(P+(n-1)Q)v^{n-1}$
2. $$
\begin{align}
\frac Av-A&=Ai\\
A(\frac 1v -1)&=P(1-v^n)+v\sum^{n-1}_{i=0}Qv^i - Qnv^n\\
&=P(1-v^n)+Q\frac{(1-v^{n})v}{1-v}-Qnv^n\\
&=P(1-v^n)+Q\frac{1-v^n}{i}-Qnv^n\\
&=P(1-v^n)+Q(\frac{1-v^n}{i}-nv^n)\\
A&=P\frac{1-v^n}i+\frac Qi(\frac{1-v^n}{i}-nv^n)\\
&=P\cdot a_n\urcorner,i+\frac Qi(a_n\urcorner,i-nv^n)
\\\\where\\
a_n\urcorner,i&:=\frac{1-v^n}i
\end{align}
$$
