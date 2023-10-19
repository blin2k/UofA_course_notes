One-Factor: [[Topic 3 (Analysis of Several Population Means)#^476915]]


---
# Part 1

Parameters of Interest: $\{\mu_i\}^k_{i=1}$
- Several means

Assumption:
- Independent random samples
- Normal population
- Equal variability
	- $\forall\quad i,j\in(1,k)\qquad\sigma_i^2=\sigma_j^2$

---
## One-Factor ANOVA F-test

Are there any differences among the k population means?

Test Setup
- $H_0:\mu_1=\mu_2=...=\mu_k$
	- One-Mean Model / Equal-Mean Model
- $H_a:$ Not all means are equal
	- k-Means Model / Separate-Means model

Method
	Compare the variability between ==the sample means== to the variability of ==the observations within their samples==.
 
---
### Variability Between Samples Means
	$MS_{Treatments}\Rightarrow$ Mean-Square for Treatments

$MS_{Treatments}=MS_{Tr}=\frac{SS_{Tr}}{df(Treatments)}=\frac{SS_{Tr}}{k-1}$

- Some may call this $MS_B$ for "Between", or $MS_G$ for "Groups"

---
### Variability of the Observations Within their Samples

	$MS_E\Rightarrow$ Mean-Square for Error

$MS_E=\frac{SS_E}{df(Error)}=\frac{SS_E}{n-k}$

- Some may call this $MS_W$ for "Within"

Our best estimate for $\sigma^2$:
$\Rightarrow MS_E=s_p^2=\frac{\sum_{i=1}^k (n_i-1)s_i^2}{n-k}$

---
### Method

Test-Statistic:
$\Rightarrow F_0^*=\frac{MS_{Tr}}{MS_E}=\frac{SS_{Tr}}{k-1}\cdot \frac{n-k}{SS_E}$

$F_0^*\sim F^{k-1}_{n-k}$ or $F(k-1,n-k)$
then check the F-table
- H0 were false
	- $MS_T>MS_E$
		- $F^*_0\uparrow$
- H0 were true
	- $MS_{Tr}\approx MS_E$
		- $F_0^*\downarrow$

$p-value=P(F^{k-1}_{n-k}>F_0^*)$

---
### Scheme

^476915

#### Purpose
To test for the difference between k population means.

#### Assumptions
1. Simple random samples from each population (independent within population)
2. Independent samples (independent among samples)
3. All populations are normally distribution OR samples are large
4. Equal population standard deviations

#### Step1
Check assumptions

#### Step2
State the hypotheses H0 and Ha

#### Step3
$SS_{Tr}=\sum\sum(\bar y_j-\bar {\bar y})^2=\sum n_j(\bar y_j-\bar{\bar j})^2$
$SS_E=\sum\sum(y_{ij}-\bar y_j)^2$
$SS_{Total}=\sum\sum(y_{ij}-\bar{\bar j})^2=SS_{Tr}+SS_E$

$F=\frac{SS_T}{k-1}\cdot\frac{n-k}{SS_E}$

#### Step 4
$F_{n-k}^{k-1}$
or
$df=(k-1,n-k)$

check the p-value

#### Conclusion
skip

---
# Multiple Combinations
- Unplanned comparisons

==If and only if==, one-way ANOVA results in rejecting the H0, then it is often desirable to do multiple comparations to determine ==which means are different the which other means.==

Multiple Comparations: $C^2_k=\frac{k(k-1)}{2}$
- Tukey Multiple Comparations (HSD = Honest Significant Difference)
	- Require the sample sizes to be the same
	- equal sample size -> shorter Confidence Interval -> more likely to show differences
- Bonferroni Method
	- For general case where sample size are different
	- Control the overall error rate
- Fisher Method
- Scheffe Method
	- Wider Confidence Interval than Tukey's test, therefore more conservative
- Least Significant Difference (LSD)
	- Not suitable if the number of groups being compared is large
- Student-Newman-Keuls test (SNK)

---
## Tukey Multiple Comparations

- Purpose
	- determine pairwise differences between k means when the H0 has been rejected in one-way ANOVA
- Assumptions
	- same as for one-way ANOVA
- Interpreting the output
	- declare two means are different if the CI does not contain 0
- Means Comparisons Diagram
	- rank the  means from smallest to largest
	- connect those groups that can not be declared different
- Conclusion

---
## Bonferroni's Method

- Purpose
	- determine pairwise differences between k means when H0 has been rejected in one-way ANOVA
1. Find the number of multiple comparisons that are possible
	1. $\frac{k\cdot(k-1)}{2}$
2. Calculate the individual comparison-wise error rate $\alpha_I$ based on experiment-wise error rate $\alpha_F$ or confidence level ($1-\alpha_F$)
	1. $\alpha_I=\frac{\alpha_F}m$
3. Find the critical value of t and df=n-k for $\frac{\alpha_I}2$
	1. $t_{\frac{\alpha_I}{2}},df$
4. Calculate the margin of error for each comparison
	1. $ME_{ij}=CV\times SE(\bar y_i-\bar y_j)=t_{\frac{\alpha_I}2,n-k}\times \sqrt{MS_E}\cdot\sqrt{\frac1{n_i}+\frac1{n_j}}$
5. Compile the results in a matrix
	1. $\mu_i-\mu_j\not=0,if\,|\bar y_i-\bar y_j|\ge ME_{ij}$
	2. ![[Pasted image 20231015165907.png]]
6. Means comparisons diagram
	1. ![[Pasted image 20231015165947.png]]
	2. ranking the sample means from smallest to largest and by connecting with lines those whose population means were not declared different
7. Conclusion

---
# Linear Combinations 
- Contrasts
- Planned Comparisons

==If and only if==, one-way ANOVA rejects the H0, then we perform linear contrasts (or multiple comparisons)

1. Develop the linear combination by deciding which means or groups of means you want to compare
	1. $\gamma_{D-E}=\frac{\sum\mu_{1.i}}d-\frac{\sum\mu_{2.j}}e$
	2. define the parameter of the contract
		1. $\gamma=\sum C_i\mu_i$
			1. the difference between the average of some groups and the average of some other groups
		2. $\sum C_i=0$
2. State the hypothesis
	1. $H_0:\gamma=0$
	2. $H_a:\gamma \not=/>/<0$
3. Calculate the estimate (sample contrast), standard error of the estimate and the t-statistic
	1. estimate $\hat \gamma=\sum C_i\mu_i$
	2. $SE(\hat \gamma)=s_p\sqrt{\sum\frac{C_i^2}{n_i}}$
		1. $s_p=\sqrt{MS_E}=\sqrt{\frac{\sum(n_i-1)s_i^2}{n-k}}$
	3. $t=\frac{\hat \gamma-0}{SE(\hat \gamma)}$
4. Compare the p-value at df=n-k with $\alpha$
5. Conclusion

### Confidence Interval for a Linear Contrast
1. For a given confidence level $1-\alpha$, find the critical value $t_{\frac\alpha 2,df=n-k}$
2. Calculate
	1. parameter $\gamma=\sum C_i\mu_i$
	2. estimate $\hat \gamma=\sum C_i\bar y_i$
	3. SE($\hat\gamma$)
		1. $s_p$
	4. CI: $\hat \gamma \pm CV\times SE$
3. Interpretation

---
# Extra Sum-of-Squares F-test in Single-Factor ANOVA

Classifies two models
- reduced model
	- H0 is the reduced model, which is a special case of the full model obtained by imposing some restrictions
- full model
	- Ha is the full model, which is a general model that is found to adequately describe the data

---
## Extra Sum-of-Squares F-test

1. Null and alternative hypothesis
	1. H0: reduced model
	2. Ha: full model
2. Calculations for Extra Sum-of-Squares F-test
	1. Extra Sum of Squares=$SS_E(reduced)-SS_E(full)$
	2. Extra df = $df_E(reduced)-df_E(full)$
	3. $F=\frac{extra\, SS}{extra\, df}\cdot \frac{df_E(full)}{SS_E(full)}$
		1. $\frac{SS_E(reduced)-SS_E(full)}{df_E(reduced)-df_E(full)}\cdot \frac{df_E(full)}{SS_E(full)}$
3. Examine the distribution of the F-table
	1. $df = [extra\,df,df_E(full)]=[extra\,df,n-k]$
4. $SS_E=\sum(y_i-\bar y)^2$
	1. residual (error) = observed value - estimated value, thus the residual sum of squares goes like this

---
# The Kruskal-Wallis test
Non-parametric Equivalent of One-Way ANOVA

- can be used in all situations where there are k>2 independent samples
- if the data fit the assumptions of ANOVA, the Kruskal-Wallis Test will be $\frac3\pi=95.5\%$ as powerful as ANOVA
	- if not, the KWT will be ==more powerful== than ANOVA
- the data are ranked in order from lowest to highest and calculations are performed on ranks
- where there are tied observations, assign the average rank to the tied observations

If
- one or more of the data sets being compared are not normally distributed nor are they log-normal
- when the one or more sample sizes are less than  30 (CLT)

the KWT is ==the only valid option==
- which means, one-factor ANOVA cannot be performed

Also, since the KWT converts the raw data to ranks, it is ==not affected by outliers== or unequal standard deviations, while these affect one-way ANOVA.

---
1. Purpose
	1. to test for a difference between k populations where k>2
2. Assumptions
	1. SRS
	2. independent samples
	3. same-shape population
	4. all sample sizes greater or equal to 5
3. Hypothesis
	1. H0: the population distributions of k populations are identical
	2. Ha: the population distributions of k populations are not identical, that is, at least two are different
4. Calculating the test statistic
	1. rank the data from lowest to highest
	2. $H=\frac{12}{n\cdot(n+1)}\sum^k_{j=1}\frac{R_j^2}{n_j}-3(n+1)$
		1. $R_j$: the sums of the ranks for the sample j data
		2. $n_j$: the samples sizes of samples j
	3. critical values of $H$ follow the $\mathcal X^2_\alpha$ distribution with df=k-1