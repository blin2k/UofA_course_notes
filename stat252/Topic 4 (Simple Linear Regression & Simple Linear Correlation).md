Goal:
- analyze the relationship between ==quantitative== variables
- simple
	- only two variables

# Scatterplot
- placing points on the graph that correspond to the values of both variables at the same time
- data points roughly fall in a straight line
	- probably a linear relationship between the two variables

# SLR
- analyze the relationship between two quantitative variables when one variable responds to the other
	- explanatory variable (predictor variable)
		- on x-axis
		- the variable that may affect the other variable or that can be used to make predictions about the other variable
	- response variable
		- on y-axis
		- the variable that reacts to or is affected by the explanatory variable
		- responds to changes in the predictor variable
---
## Model
### For Population
$\mu(Y|X)=\beta_0+\beta_1X$
- $\beta_0$
	- the y-intercept
- $\beta_1$
	- the slope

### Estimated Model
$\hat y=\hat \mu(Y|X)=\hat\beta_0+\hat\beta_1 x$
- $slope=\hat\beta_1=\frac{S_{xy}}{S_{xx}}=\frac{\sum(x_i-\bar x)(y_i-\bar y)}{\sum(x_i-\bar x)^2}$
- $y-intercept=\hat\beta_0=\bar y-\hat\beta_1 \bar x=\frac{\sum y}n-\hat\beta_1\frac{\sum x}n$
---
## Three Sum of Squares
- $SS_{TOTAL}=SS_{yy}=\sum(y_i-\bar y)^2$
- $SS_{REGR}=\sum(\hat y_i-\bar y)^2=\frac{S_{xy}^2}{S_{xx}}$
	- between $\hat y$ and $\bar y$
- $SS_{ERROR}=SS_{RES}=\sum(y_i-\hat y_i)^2$
	- $=SS_{TOTAL}-SS_{REGR}$
		- regression identity
	- outside $\hat y$ and $\bar y$

---
## Analysis
- $error(e)=y_i-\hat y_i$
	- vertical distance from the regression line to a data point
	- could be positive or negative
- $SS_{RES}=SS_{ERROR}=SS_{TOTAL}-SS_{REGR}=\sum(y_i-\hat y_i)^2$

Least-squares Criterion
	Tries to minimize SSE in order to get the best fit line

- $S_e=\hat \sigma=\sqrt{\frac{\sum e^2}{n-2}}=\sqrt{\frac{\sum (y_i-\hat y_i)^2}{n-2}}=\sqrt{\frac{SSE}{n-2}}=\sqrt{MSE}$

Interpolation
- predict within the range of data
Extrapolation
- predict outside the range of data

---
## Assumptions
1. linearity
	1. population regression in line
2. homoscedasticity
	1. equal SD
3. normal populations
4. independent observations
---
## Regression ANOVA Test
- $MS_{REGR}=\frac{SS_{REGR}}{1}$
	- the denominator is $df_{REGR}-1=2-1=1$
- $MS_{ERROR}=\frac{SS_{ERROR}}{n-2}$
	- the denominator is $df_{ERROR}=n-2$
- $F=\frac{MS_{REGR}}{MS_{ERROR}}=\frac{SS_{REGR}}{SS_{ERROR}}\cdot\frac{n-2}{1}$
---
1. select appropriate test by checking purpose and assumptions
2. $H_0:\beta_1=0$
	1. $H_a:\beta_1\not=0$
3. calculate $F$
4. decide to reject or not
	1. $df=(1,n-2)$
5. conclusion

### Note
- $MS_{ERROR}=\hat\sigma^2$
- $t^2=F$
- the p-value will be the same for ==both the F-test and the two-tailed t-test==
---
## Inferences for the Slope
- in SLR, either a t-test or ANOVA can be used to test the slope
- however, t-test is more flexible
	- suitable for doing two-tailed tests or one-tailed tests

Purpose
	To determine whether there is a relationship, or, to decide whether the slope is significantly different from 0

Assumptions
	skip

Steps
1. select
2. $H_0:\beta_1=0$
	1. $H_a:\beta_1\quad\not=/</>\quad0$
3. calculate
	1. $SS_{TOTAL}=S_{yy}$
	2. $SS_{REGR}=\frac{S_{xy}^2}{S_{xx}}$
	3. $SS_{ERROR}=SS_{TOTAL}-SS_{REGR}$
	4. $\hat\sigma=\sqrt{\frac{SS_{ERROR}}{n-2}}=\sqrt{MS_{ERROR}}$
	5. $SE(\hat\beta_1)=\frac{\hat\sigma}{\sqrt{S_{xx}}}$
		1. $S_{xx}=(n-1)s_x^2$
	6. $t=\frac{\hat\beta_1}{SE(\hat\beta_1)}$
4. decide to reject or not
	1. $df=n-2$
5. conclusion

- $CI=\hat\beta_1\pm t_{\frac \alpha2}\cdot SE(\hat\beta_1)$
----
## CI for Mean Response of y

Purpose
	To find a CI for the mean response for any given x

Assumptions
	The 4 assumptions for regression inferences

Steps
1. find $t_{\frac\alpha2}$ at $df=n-2$
2. compute
	1. $\hat y=\hat\beta_0+\hat\beta_1 x^*$
	2. $CI=\hat y\pm t_{\frac\alpha2,n-2}\cdot\hat\sigma\sqrt{\frac1n+\frac{(x^*-\bar x)^2}{S_{xx}}}$
		1. $S_{xx}=(n-1)S_x^2$
3. interpret

### PI for All Single Observations of y for x
Prediction Interval

Same as above, but
$PI=\hat y\pm t_{\frac\alpha2,n-2}\cdot\hat\sigma\sqrt{1+\frac1n+\frac{(x^*-\bar x)^2}{S_{xx}}}$

---
# SLC
- analyze the relationship between two quantitative variable when a change in one variable appears to be related to a change in the other, ==but one is not necessarily responding to the other==
	- co-related
	- either variable may be plotted as x or y
	- can be applied to wider variety of situations
		- even when the variables cannot be identified as explanatory and response variables

---
## Three Aspects of a Relationship Between Variables

	r is the value of Linear Correlation.

	$R^2$ is Coefficient of Determination.

- direction
	- positive correlation
		- if r is positive, then the slope must be positive
	- negative correlation
		- if r is negative, then the slope must be negative
- form
	- linear
		- straight line
	- curved
- strength
	- |r| ~ 1
		- strong linear relationship
	- |r| ~ 0
		- no or weak relationship
---
## Warnings
- outlier
- leverage
	- data point whose x-value is far from the mean of x
	- affecting the linear regression line
	- can completely change the slope and y-intercept
- influential point
	- a data point which, if omitted, results in a very different regression model
---
## Calculation
$r=\frac{\text{covariance of x and y}}{(SD(x))(SD(y))}$
- $cov(x,y)=\frac{\sum(x_i-\bar x)(y_i-\bar y)}{n-1}$

$r=\frac{S_{xy}}{S_x\cdot S_y}=\frac{\sum(x_i-\bar x)(y_i-\bar y)}{n-1}\cdot\frac{1}{\sqrt{\frac{\sum(x_i-\bar x)^2}{n-1}}\cdot\sqrt{\frac{\sum(y_i-\bar y)^2}{n-1}}}$
$r=\frac{S_{xy}}{\sqrt{S_{xx}\cdot S_{yy}}}$

$r=\sqrt{\frac{SS_{REGR}}{SS_{TOTAL}}}$
- then ==add correct sign== + or -

$R^2=r^2=\frac{SS_{REGR}}{SS_{TOTAL}}$

$R^2_{adjusted}=1-\frac{MSE}{MST}$

---
## Hypothesis Test
Purpose
	To decide whether two variables are significantly correlated.

Steps
1. select
2. $H_0:\rho=0$
	1. $H_a:\rho\quad\not=/</>\quad 0$
	2. $\rho:$ population correlation coefficient
3. compute $r$
	1. $r=\frac{s_{xy}}{s_x\cdot s_y}=\frac{S_{xy}}{\sqrt{S_{xx}\cdot S_{yy}}}=\sqrt{\frac{SS_{REGR}}{SS_{TOTAL}}}$        (add correct sign, + or -)
4. decide to reject or not
	1. $df=n-2$
5. interpretation

---
