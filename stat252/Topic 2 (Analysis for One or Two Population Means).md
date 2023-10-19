# Part 1

## population & sample
- population (parameters)
	- not likely to collect
	- true value
- sample (statistics)
	- approachable
	- estimation of the true value
		- within a certainty
## statistical inference & SD/SE
- statistical inference
	- drawing conclusions about population based on information collected in samples

	The sample mean, $\bar Y=\frac1n\sum^n_{i=1}Y_i$, will be used to estimate the population mean $\mu_{\tiny Y}$ 

- standard deviation of the estimate $S.D(\bar Y)=\sigma_{\bar {{Y}}}=\frac{\sigma_Y}{\sqrt n}$
	- unknown parameter and must be estimated
- standard error of the estimate $S.E(\bar Y)=\hat\sigma_{\bar {{Y}}}=\frac{S_Y}{\sqrt n}$
	- the estimated SD, based on the sample

we need to know the numerator first to compute the mean value, however, the true value for population is unknown, so we take SE of the sample to estimate the mean SE for samples, then take that value to estimate the SD.
## sample distribution
- sample distribution
	- the probability distribution of an ==estimate==, based on a sample
	- $Y \sim Normal(\mu_Y,\sigma^2_Y)\rightarrow \bar Y \sim Normal\left(\mu_{\bar Y}=\mu_Y,\sigma^2_{\bar Y}=\frac{\sigma^2_Y}{n}\right)$
		- $\mu_{\bar Y}=\mu_Y$ means the estimate $\bar Y$ is ==unbiased== for the parameter $\mu_Y$

- central limit theorem
	- large sample size $n$ $\rightarrow$ $\bar Y \approx Normal$

 - rule of thumb
	 - not heavily skewed $\rightarrow$ at least 30 observation is sufficient

---
## Z-ratio

standardize:
$$\begin{align}Z-ratio&=\frac{Estimate-Mean(Estimate)}{S.D.(Estimate)}\\&=\frac{Estimate-Parameter}{S.D.(Estimate)}\\&\sim Normal(\mu_Z=0,\sigma^2_Z=1)\end{align}$$

## T-ratio
$$
\begin{align}
T-ratio&=\frac{Estimate-Mean(Estimate)}{S.E.(Estimate)}\\
&=\frac{Estimate-Parameter}{S.E.(Estimate)}\\
&\sim t_{n-1}
\end{align}
$$
	under suitable conditions, it can be shown that $T-ratio\sim t_{df}$
	follows a t-distribution with $df$ degree of freedom

- $df$= total sample size - the # of parameters in the model for $\mu_Y$

## Z vs. $t_{df}$

- both distribution are
	- symmetric
	- bell-shaped
	- with a mean of 0
- $t_{df}$ has a bit more variability
	- as $df$ increases, $t{df}$ becomes closer to Z
		- $t_\inf\sim Z$

---
## T-critical value

$P(t_{df}>t^*_{df,c})=c$
- right-tail cut-off

---
# Part 2
## confidence interval

- $(1-\alpha)100\%$ two-sided
- $P(L<parameter<U)=1-\alpha$
	- $1-\alpha$ will be called our ==confidence level== or success rate
	- $\alpha$ is our ==error rate==
		- common value: 0.01, 0.05, 0.10

$$
\begin{align}
P\left(-t^*_{df,\frac\alpha2}<\frac{Estimate-Parameter}{SE(Estimate)}<t^*_{df,\frac\alpha2}\right)&=1-\alpha\\
P\left(Estimate-t^*_{df,\frac\alpha2}\times{SE(Estimate)}<{Parameter}<Estimatet^*_{df,\frac\alpha2}\times{SE(Estimate)}\right)&=1-\alpha\\
\end{align}
$$

$\therefore$ confidence interval is $Estimate\pm \{t^*_{df,\frac\alpha2}\times{SE(Estimate)}\}$  
- = $Estimate\pm \{C.V.\times SE(Estimate)\}$
- = $Estimate\pm \{M\}$
	- $M$ stands for the Margin of Error
 ---
# Part 3
## T-tools Hypothesis Test
	To compare two competing claims (hypotheses) about our unknown parameters.
 
$\rightarrow$ Null Hypothesis vs. Alternative Hypothesis  
- null hypothesis ($H_0$)
	- parameter ==equal to== a particular value indicating ==no effect, no difference, no consequence==
		- parameter = hypothesis value
- alternative hypothesis ($H_a$)
	- parameter ==in a range== indicating ==some effect, some difference, some consequence==
		- parameter > hypothesis value
			- right-tailed test
			- p-value = $P(t_{(df)}>t^*_0)$
		- parameter < hypothesis value
			- left-tailed test
			- p-value = $P(t_{(df)}<t^*_0)$
		- parameter $\not =$ hypothesis value
			- two-tailed test
			- p-value = $2P(t_{(df)}>|t^*_0|)$

## P-value
1. assume $H_0$ is true
2. collect data
3. measure the strength of the data against $H_0$ in favour of $H_a$

p-value
- the measure for the strength of the evidence against $H_0$ in favour of $H_a$

$$
\begin{align}
T-ratio&=\frac{Estimate-Parameter}{S.E.(Estimate)}\\
&=\frac{Estimate-H_0}{S.E.(Estimate)}
\end{align}$$

- <0.01
	- convincing to strong evidence against $H_0$
- $(0.01,0.05)$
	- strong to moderate evidence 
- $(0.05,0.1)$
	- moderate to suggestive, but inconclusive
- >0.1
	- weak

## Statistical Significance
- $\alpha$ = significance level
	- = P(rejecting H0 given that H0 is true)
	- = P(Type I Error)

1. choose a value for $\alpha$
	1. 0.01 / 0.05 / 0.10
2. calculate the p-value and compare it with $\alpha$
	1. p-value < $\alpha$
		1. significant evidence against H0 in favour of Ha, at level $\alpha$
		2. reject H0 in favour of Ha, at level $\alpha$
	2. p-value  $\ge\alpha$
		1. insignificant evidence
		2. fail to reject H0, at level $\alpha$
			1. not saying that H0 is true but accept it for now

---
# Part 4
## T-tools for $\mu_1-\mu_2$

- two sample t-tools for the difference between two population means
- ==parameter==: $\mu_1-\mu_2$

depending on how the samples are collected,
we have two situations:
1. dependent (paired)
	1. t-tools application 2
2. independent
	1. t-tools application 3

---
### dependent samples
- dependent samples result when the data are ==matched pairs==
	- each subject in one sample is matched with a subject in the other sample
- ==parameter==: $\mu_d=\mu_1-\mu_2$
### independent samples
- ==parameter==: $\mu_1-\mu_2$
- estimate: $\bar Y_1-\bar Y_2$ (difference between sample means)
- assumption: the population variances are equal
	- $\sigma_1^2=\sigma_2^2$
$$\begin{align}
SD(\bar Y_1-\bar Y_2)&=\sigma_{\bar Y_1-\bar Y_2}\\
&=\sqrt{\frac{\sigma_1^2}{n_1}+\frac{\sigma_2^2}{n_2}}\\
&=\sigma\sqrt{\frac1{n_1}+\frac1{n_2}}\\
\\
SE(\bar Y_1-\bar Y_2)&=\hat\sigma\sqrt{\frac1{n_1}+\frac1{n_2}}\\
&=S_p\sqrt{\frac1{n_1}+\frac1{n_2}}\\
\end{align}
$$

where $S_p=\sqrt{\frac{(n_1-1)s_1^2+(n_2-1)s_2^2}{n_1+n_2-2}}$

---
- (1-$\alpha$)100% Confidence Interval for $\mu_1-\mu_2$
	- $(\bar y_1-\bar y_2)\pm t^*_{n_1+n_2-2,frac\alpha2}\times S_p\sqrt{\frac1{n_1}+\frac1{n_2}}$
 
- H0: $\mu_1-\mu_2=\mu_0$
	- $\frac{(\bar y_1-\bar y_2)-\mu_0}{S_p\sqrt{\frac1{n_1}+\frac1{n_2}}}$
---
# Part 5
## Normality

Normal Probability Plots
- look for  the observations to fall reasonably close to the green line
- strong deviations from the line indicate non-normality
![[Pasted image 20230924185132.png]]

Histogram
- look for a bell-shape
- severe skewness and/or outliers are indications of non-normality

Boxplots
- hard to detect normality
- look for symmetry
- severe skewness and/or outliers are indications of non-normality

## Equal Variability
![[Pasted image 20230924185520.png]]
