### Measuring Time Periods
- $t = 360(Y_2-Y_1)+30(M_2-M_1)+(D_2-D_1)$ 

	Sometimes, the interest earned over the fractional part of a period is calculated using simple interest.
- $FV=PV(1+i)^{\lfloor t\rfloor}(1+i(t-\lfloor t\rfloor)$

### Equations of Value
	A person must pay CAD 7000.00 at the end of nine years. In return for that promise, she/he agrees to pay CAD 1000.00 now, CAD 4000.00 at the end of six years, and to make an additional payment at the end of eleven years. Assume a nominal rate of annual interest of 6.0 % compounded semi-annually. Calculate the required final payment.

1. i = 0.06/2 = 0.03
	1. v = 1/1.03
2. $7000v^{18}=1000+4000v^{12}+xv^{22}$ 
	1. v is the discount factor
	2. we are tracing back the value at the common date for comparison
3. solve for x

### Unknown Time
Find the equivalent time that paid at once
$$
\begin{align}
\sum^n_{k=1}p_k\cdot v^{t_k}&=(\sum^n_{k=1}p_k)v^t\\
&\downarrow\\
t&=\frac{ln(\frac{\sum^n_{k=1}p_kv^{t_k}}{\sum^n_{k=1}p_k})}{ln(v)}
\end{align}
$$

### Increasing the Investment
Trying to find time t1 that $PVa(t_1)=k\cdot PVa(t_0)$ 
- $\Delta t=t_1-t_0=\frac{ln(k)}{ln(1+i)}$ 

Given a factor k and a period of time, find the interest rate
- $i=e^{\frac{ln(k)}{\Delta t}}-1$ 

### Deposits & Withdrawals
	On February 2nd, 2017, an account earning 5.0% annual interest compounded annually was opened with a deposit of CAD 10,000.00 Two years later, a withdrawal of CAD 5000.00 was made. Three years after that, a deposit of CAD 1500.00 was made. Calculate the balance in the account today, February 2nd, 2023.

$10000(1+0.05)^6−5000(1+0.05)^4+1500(1+0.05)^1$ 