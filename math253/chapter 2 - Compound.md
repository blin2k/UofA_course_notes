	Interest Paid (interest earned) = I = FV - PV

### Accumulation Function
$a:[0,\infty)\rightarrow \mathbb R$
	Consider a customer who invests 1 monetary unit (1 CAD) of principal.
	a(t) = accumulated value of 1 monetary unit after y years

### Amount Function
$A(t)=P_0\cdot a(t)=FV$ 

### Amount of Interest
$I_n$ = amount of interest earned during the n-th period (from t=n-1 to t=n)
    =A(n) - A(n-1)

### Effective Rate of Interest
$$\begin{align}
i_n&=a(n)-a(n-1)\\
&=\frac{A(n)-A(n-1)}{A(n-1)}\\
&=\frac{I_n}{A(n-1)}
\end{align}$$
$\frac{\text{Ending Balance - Starting Balance}}{\text{Starting Balance}}$

---
### Simple Interest
- $a(t) = 1+it$
- $A(t) = FV = PV(1+it)$

### Compound Interest
- $a(t) = (1+i)^t$
- $A(t)=PV(1+i)^t$

---
### Fill by Comparing
	Suppose that CAD 1000.00 invested at time 0 accumulates to CAD 3000.00 by time 7. We want to find the value of the investment at time t = 10 of CAD 5000.00 invested at time 5.

$A(t_2)=\frac{a(t_2)}{a(t_1)}A(t_1)$

### Trace Back

$PV = \frac {FV}{(1+i)^t}=FV\cdot v^t$
- We call $v=\frac 1 {1+i}$ the DISCOUNT FACTOR

#### Quarterly Compounding
	If the interest is expressed using a quarter year as the time period
	adjust the times it compounding

$t' = t\cdot 4$

---
### Nominal Rate of Interest & Effective Rate of Interest
- monthly interest rate of 2%
	- $i^{(m)}=12\cdot2\%=24\%$
	- $i=(1+2\%)^{12}-1=26.82\%$ 

- $i^{(m)}$ is the nominal rate of interest for a period when interest is payable m times per peroid
- $\frac{i^{(m)}}{m}=$ interest per period
- $i=(1+\frac{i^{(m)}}{m})^m-1$ is the effective rate of interest for that period

### Discount Rates
	Sometimes interest is paid at the inception of the loan, rather than at the end.

effective rate of discount: 
- $i=\frac d{1-d}$ 
- $d=\frac i{1+i}=1-v$

then
- $FV=PV(1+i)^t=PV(1-d)^{-t}=PVv^{-t}$
- $PV=FV(1+i)^{-t}=FV(1-d)^t=FVv^t$

### Nominal Rate of Discount
$1-d=(1-\frac{d^{(p)}}{p})^p$ 
$\rightarrow (1+\frac{i^{(m)}}{m})^{mt}=(1+i)^t=(1-\frac {d^{(p)}}p)^{-pt}$ 

---
### Force of Interest and Force of Discount
- $\delta(t)=\frac{a'(t)}{a(t)}=\frac{A'(t)}{A(t)}$ 
	The force of interest is the relative rate of change of the accumulation function a, also the relative rate of change of the amount function A

- $a(t)=e^{\int^t_0\delta(s)ds}$
	- Given $\delta$, derive $a(t)$
 - $\delta(t)=ln(1+i)=ln(\frac1v=-ln(v))$
	 - compound

#### Continuous Compounding
$$\begin{align}
\underset{m\rightarrow\infty}{lim}a(t;m)&=\underset{m\rightarrow\infty}{lim}(1+\frac im)^{mt}\\
&=e^{it}
\end{align}$$
- $a(t)=e^{it}$
- $A(t)=A(0)e^{it}$
- $FV=PVe^{it}$

Specially, $a(t)=(1+i)^t=e^{ln(1+i)t}$, therefore, when the continuous compounding rate is ln(1+i), it grows the same like effective annual rate of interest of i.

### Force of Discount
Discount Function: $\frac 1{a(t)}$
Thus, $\delta'(t)=-\frac{\frac d{dt}\frac 1{a(t)}}{\frac1{a(t)}}=\frac{\frac d{dt}a(t)}{a(t)}=\delta(t)$ 

