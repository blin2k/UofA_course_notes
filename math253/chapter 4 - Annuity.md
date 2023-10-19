### Definition
Fixed Term Level Payment Annuity
	"An annuity that pays CAD 400.00 every month for five years."
	The term of an annuity can be given in years or as the number of payments. Thus, an annuity that pays CAD 400.00 every month for five years has a term of five years or sixty months.

Annuity-Certain
	An annuity-certain is an annuity that consists of payments that are certain to be made for a prescribed period.

Term
	The term of an annuity is the duration of the annuity in payment periods. An annuity that provides payments each month for sixty months has a monthly period and a term of 60 (months). A “perpetuity” is an annuity that offers an infinite sequence of payments.

Annuities-Immediate
	An annuity-immediate is an annuity in which payments are made at the end of each period.

Annuities-Due
	An annuity-due is an annuity in which payments are made at the beginning of each period.

### Annuities-Immediate
### Calculate the Value at the Time of its Inception
term pay 1 CAD:
- The k-th payment: $v^k$
- The total value: $a_n\urcorner,i=\sum_{k=1}^nv^k=\frac{1-v^n}{i}$ 

term pay R CAD:
- The k-th payment: $Rv^k$
- The total value: $Ra_n\urcorner,i=R\sum_{k=1}^nv^k=\frac{1-v^n}{i}$ 

$a_n\urcorner,i$: PV of an Annuity-Immediate of CAD 1 per period for n periods
$s_n\urcorner,i$: FV of an Annuity-Immediate of CAD 1 per period for n periods
$$\begin{align}
s_n\urcorner,i&=FV\\
&=PV(1+i)^n\\
&=a_n\urcorner,i(1+i)^n
\end{align}$$
$FV=PV(1+i)^n=Ra_n\urcorner,i(1+i)^n=Rs_n\urcorner,i$

$\frac1{s_n\urcorner,i}+i=\frac1{a_n\urcorner,i}$ 

### The Price of an Annuity
If the annuity is purchased at the start of the first period, the payment of the annuity in terms of its price (PV) is $R=\frac {PV}{a_n\urcorner,i}$ 

---
### Annuities-Due

effective rate of discount: $d=\frac i{1+i}=iv$
$\sum^{n-1}_{j=0}au^j=a\frac{1-u^n}{1-u}$

- The k-th payment at inception: $v^{k-1}$
- The total value: $\ddot a_n\urcorner,i=\sum^{n-1}_{k=0}v^k=a_n\urcorner,i(1+i)=\frac{1-v^n}d$ 
- $\ddot s_n\urcorner,i=\ddot a_n\urcorner,i(1+i)^n=\frac{(1+i)^n-1}d$ 
---
### The Value of an Annuity at any Date
1. before inception
	1. m years prior to inception: $v^mRa_n\urcorner,i=Ra_{m+n}\urcorner,i-Ra_m\urcorner,i$
2. after final payment
	1. m periods after the final payment: $FV=Rs_n\urcorner,i(1+i)^m=Ra_n\urcorner,i(1+i)^{n+m}$
3. between inception and the last payment
	1. m periods after inception: $Ra_n\urcorner,i(1+i)^m=Rs_n\urcorner,iv^{n-m}=Ra_{n-m}\urcorner,i$
---
### Perpetuities
	A perpetuity is an annuity in which the payments continue forever.
- perpetuity-immediate
	- $a_\infty\urcorner=\sum^infty_{j=1}v^j=\frac1i$
	- $PV=Ra_\infty\urcorner=\frac Ri$
- perpetuity-due
	- $\ddot a_\infty\urcorner=\sum^\infty_{j=0}v^j=\frac1d$
	- $PV=\frac Rd$

$\sum^\infty_{j=0}au^j=a\frac1{1-u}$

	George has USD 2,000,000. Payments will be paid monthly at nominal annual rate of 12% compounded monthly.
	Mary receives the first 10 years, John receives the next 15 years, NYU receives all additional.

Mary: 
- payments: $n=10 \times 12 = 120$
- each payment: $R=2000000 \times\frac{0.12}{12}=20000$
- $PV=Ra_n\urcorner,i$

John
- n=180
- R
- $PV=Ra_n\urcorner,iv^{120}$
	- discount 10 years = 120 payments

NYU
- $Ra_\infty\urcorner v^{300}=\frac Riv^{300}$
	- discount 25 years = 300 payments

### Varying Interest Rate
$i_j$: interest rate in period j (from time j-1 to j)

- forward rates
	- $i_k=f_k$ in period k
	- $PV=R\sum^n_{j=1}\prod^j_{k=1}(1+f_k)^-{1}$
- spot rate
	- every payment has its own private interest rate
	- $i_k=g_k$
	- $PV=R\sum^n_{k=1}(1+g_k)^{-k}$ 

### Annuities Payable at Different Frequencies than Interest is Convertible
	We consider the case where the period of the payments is different from the conversion period of the interest. One method is to convert the conversion period of the interest to the period of the payments.

- pays at the end of each quarter
- rate is compounded monthly

-  $1+i=(1+\frac{i^{(12)}}{12})^3$ 
	- 12: year to month
	- 3: month to quarter

- pays at the end of each quarter
- derive effective annual rate

- $1+j=(1+i)^4$
	- i is the effective quarterly rate
	- 4: quarter to year

### Annuities Payable Less Frequencies than Interest is Convertible
- k: interest conversion periods in one payment period (compound per period)
- n: period of the annuity in interest conversion periods (total compound)
- i: interest rate per interest conversion period

number of payments = $\frac nk$ 

	Consider an annuity that pays CAD R every quarter. The life of the annuity is seven years. The interest is converted monthly.

- k = 3
- n = 7x12=84
- n/k = 28 = 7x4

Annuity-Immediate
- $PV=\sum^{\frac nk}_{i=1}Rv^{ik}=R\frac{a_n\urcorner,i}{s_k\urcorner,i}$ 
- $FV=R\frac{s_n\urcorner,i}{s_k\urcorner,i}$

Annuity-Due
- $PV=\sum^{\frac nk}-1_{i=0}Rv^{ik}=R\frac{a_n\urcorner,i}{a_k\urcorner,i}$
- $FV=R\frac{s_n\urcorner,i}{a_k\urcorner,i}$

### Annuities Payable More Frequently than Interest is Convertible
- m: number of payments made during each interest conversion period
- n: period of the annuity in interest conversion periods
- i: interest rate per interest conversion period

- number of payments: nm
- amount of each payment: R/m
- $a_{\bar n}^{(m)}$: PV of an annuity-immediate that pays CAD 1/m at the end of each payment period
	- $=1/m(\sum^{nm}_{i=1}v^\frac im)=i\frac{a_n\urcorner,i}{i^{(m)}}$
- $i^{(m)}=m[(1+i)^{\frac 1m}-1]$
- $s_{\bar n}^{(m)}$: FV
	- $i\frac{s_n\urcorner,i}{i^{(m)}}$

	Consider an annuity-immediate that pays CAD 900.00 at the end of each month for three years. The interest rate is a nominal 8% per year compounded quarterly.
- m = 3
- i = 0.08/4 = 0.02
- R/m = 900
- n = 3x4 = 12

- $\ddot a_{\bar n}^{(m)}$: at the beginning
	- $=1/m(\sum^{nm-1}_{i=0}v^\frac im)=i\frac{a_n\urcorner,i}{m[1-v^{\frac1m}]}$
- $\ddot s_{\bar n}^{(m)}=i\frac{s_n\urcorner,i}{m[1-v^{\frac1m}]}$

### Perpetuities P>I
- m: number of payments made during each interest conversion period
-  R/m: amount of each payment

- $a_{\bar \infty}^{(m)}=\frac1{i^{(m)}}$
- $\ddot a_{\bar n}^{(m)}=\frac1{v^\frac1mi^{(m)}}$
 
### Payments Varying to an Arithmetic Progression
	Consider an annuity-immediate of n payments. The interest rate per period is i. The first payment is P and the payments change by Q per period. Thus, the payments are P, P + Q, P + 2Q, · · · , P + (n − 1)Q.

$PV=\sum^{n}_{i=1}(P+(i-1)Q)v^i=Pa_n\urcorner,i+Q(\frac{a_n\urcorner,i-nv^n}{i})$ 
$FV=Ps_n\urcorner,i+Q(\frac{s_n\urcorner,i-n}i)$

### in Geometric Progression
	Consider an annuity-immediate of n payments. The interest rate per period is i. The first payment is P. The next payments increase or decrease by rate k. Thus, the payments are P, P(1 + k), P(1 + k) 2 , · · · , P(1 + k) n−1 .

$PV=\sum^{n}_{j=1}\frac{P(1+k)^{j-1}}{(1+i)^j}=\frac P{1+i}\frac{{1-(\frac{1+k}{1+i}})^n}{1-\frac{1+k}{1-i}}$
if k=i: PV = np/(1+i)

$FV=PV(1+i)^n$

---
### Payments in Blocks
	An annuity-immediate provides annual payments. The effective annual rate of interest is 5.4%. This annuity provides five payments of 300.00 Euros, then ten payments of 405.00 Euros, and then twenty-five payments of 1,500.00 Euros. Calculate the present value of this annuity.

$P V = 300.00a5⌝,i +405.00a10⌝,iv ^5 +1500.00a25⌝,iv ^15 = 12, 874.05$ 

### Perpetuties V to Arithmetic
$PV=\underset{n\rightarrow\infty}{lim}Pa_n\urcorner,i+\frac Qi(a_n\urcorner,i-nv^n)=\frac Pi+\frac Q{i^2}$

### in Geometric
$PV=\frac P{i-k}$
if k=i: $PV=\infty$

### Increasing Payments V2 Ari
	Consider an annuity-immediate of n payments. The interest rate per period is i. The first payment is P = 1 and the payments change by Q = 1 per period. Thus, the payments are P, P + Q, P + 2Q, · · · , P + (n − 1)Q, or equivalently 1, 2, 3, · · · , n.

a) We want to calculate the present value $Ia$ of this annuity. 
- $(Ia)_n\urcorner,i=a_n\urcorner,i+\frac{a_n\urcorner,i-nv^n}{i}=\frac{\ddot a_n\urcorner,i-nv^n}i$
b) We want to calculate the future value $Is$ of this annuity.
- $(Is)_n\urcorner,i=\frac{\ddot s_n\urcorner,i-n}i$

$\ddot a_n\urcorner,i=\frac 1va_n\urcorner,i$
$\ddot s_n\urcorner,i=\frac 1vs_n\urcorner,i$

### Decreasing P v2 Ari
	Consider an annuity-immediate of n payments. The interest rate per period is i. The first payment is P = n and the payments change by Q = −1 per period. Thus, the payments are P, P + Q, P + 2Q, · · · , P + (n − 1)Q, or equivalently n, n − 1, n − 2, · · · , 1.

a) We want to calculate the present value $Da$ of this annuity.
- $(Da)_n\urcorner,i=a_n\urcorner,i-\frac{a_n\urcorner,i-nv^n}{i}=\frac{n- a_n\urcorner,i}i$
b) We want to calculate the future value $Ds$ of this annuity.
- $(Ds)_n\urcorner,i=\frac{n(1+i)^n-s_n\urcorner,i}i$

	Suppose that the annual interest rate is i. Consider an annuity-immediate such that payments start at 1 CAD, increase by annual amounts of CAD 1 to a payment of n, and then decrease by annual amounts of CAD 1 to a final payment of CAD 1. Calculate the present value of this annuityimmediate.

The present value is 
![[Pasted image 20230424111914.png]]
	Suppose that the interest rate per payment period is i. Consider an annuity-immediate such that payments start at 1 CAD, each payment thereafter increases by 1 CAD until reaching 10 CAD, and then remain at that level until 15 payments in total are made. Calculate the present value of this annuity immediate.

$P V = (Ia)10⌝,i + 10v ^{10}a5⌝,i.$

### Annuities v2 Ari & paid < I
![[Pasted image 20230424113122.png]]
![[Pasted image 20230424113146.png]]
![[Pasted image 20230424113200.png]]

### Continuous Varying Annuities
	Consider an increasing annuity for n conversion period. The amount of the payment made at time t is f(t)dt. We allow the force of interest δ to vary continuously. 

Then, the present value of this continuous varying annuity is $PV=\int^n_0f(t)e^{-\int^t_0\delta(s)ds}dt$ 