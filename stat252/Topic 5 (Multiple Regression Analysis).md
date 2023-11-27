# The Multiple Linear Regression Model

- $y=\beta_0+\sum_{p=1}^P\beta_px_p+\epsilon$
- more than one explanatory or predictor variables
	- $x_1,...,x_p$
	- p = number of predictor variables
- only one response variable
	- y
- $E(y)=\beta_0+\sum\beta_px_p$
	- the deterministic part of the model
	- $\beta_i$ determines ==the contribution== of the explanatory variable $x_i$ to the model
	- $\epsilon$ is the random error
		- assumed to be normally distributed with mean 0 and standard deviation $\sigma$
  
- population multiple linear regression equation
	- $\mu(y|x_1,...,x_p)=\beta_0+\beta_1x_1+...+\beta_px_p$
- sample multiple linear regression equation
	- $\hat y=\hat\beta_0+\sum_{p=1}^P\hat\beta_px_p+\epsilon$
	- $\hat\mu(y|x_1,...,x_p)=\hat\beta_0+\hat\beta_1x_1+...+\hat\beta_px_p$
	- the y-intercept $\hat\beta_0$ is the value of y when all explanatory variables are 0
	- the values $\sum\hat\beta_p$ 
		- partial slopes / partial regression coefficients
		- each $\hat\beta$ tells us ==the change in y per unit increase in x==, holding all other explanatory variables constant 

# Inferences

## Assumptions
1. Linearity of the population regression line
2. Equal SD (homoscedasticity)
3. Normal population
4. No serious outliers
5. Independent observations
	1. response variables should be independent of one another
	2. predictor variables do not need to

## Regression Identity
- $SS_{total}=SS_{regr}+SS_{error}$
- $df(SS_{total})=df(SS_{regr})+df(SS_{error})$
	- n-1 = p + (n-(p+1))
		- n is sample size
		- p is the number of predictor variables

## Multiple Regression ANOVA Test (F-test)

- hypothesis
	- $H_0: \beta_1=...=\beta_p=0$
	- $H_a:$ at least one of the slopes $\beta_i$ is not 0
- sums of squares and f-statistic
![[Pasted image 20231126171540.png]]
- reject or not
	- df = (p, n-(p+1))
		- n = num of xy observation
		- p = num of predictor variables
- conclusion

## Multiple R (Multiple Correlation Coefficient)

- measures the overall correlation between the all the variables involved in the model
	- how fit is the model
- multiple $R=+\sqrt{R^2}$

## Coefficient of Multiple Determination
- $R^2=\frac{SS_{regr}}{SS_{total}}=1-\frac{SS_{error}}{SS_{total}}$

## Adjusted Coefficient of Determination
- $R_{adj}^2=1-\frac{SS_{error}}{SS_{total}}=1-\frac{SS_{error}}{n-(p+1)}\cdot\frac{n-1}{SS_{total}}$
- more accurate

---
# Multiple Regression t-test and Confidence Interval

## t-test
- $H_0:\beta_i=0$
	- predictor variable $x_i$ is ==not useful== in making predictions about the response variable
- $H_a:\beta_i\not=/</>0$

- $t=\frac{\hat\beta_i}{SE(\hat\beta_i)}$
- $df=n-(p+1)$

>[!notice]
>$t^2\not=F$ in multiple linear regression, though it did in simple linear regression.

## Confidence Interval for Slope i
$\hat\beta_i\pm t_{\frac\alpha2}\times SE(\hat\beta_i)$

---
# CI and Prediction Interval for the Response Variable
- $\hat y=\hat\beta_0+\hat\beta_1x_1+...+\hat\beta_px_p$
- $CI=\hat y\pm t_{\frac\alpha2}\times SE(fit)$
	- $SE(fit)=S_{\hat y_p}$
		- SD of the predicted y-value
- $PI=\hat y\pm t_{\frac\alpha2}\times\sqrt{MSE+[SE(fit)]^2}$
	- $MSE=\hat \sigma^2$
	- $SE(fit)=S_{\hat y_p}$

---
# Multiple Regression Model Involving Indicator Variables(Dummy Variables)

- categorial variables that are used as one of the predictor variables
- coded as 0 or 1
	- e.g. 0 for female and 1 for male

---
# Interaction Models
- without interaction
	- $y=\sum\beta x+\epsilon$
	- the slope remains the same when there are only two x-variables are changing
	- ![[Pasted image 20231126202505.png]]
	- with interaction
		- $y=\beta_0+\beta_1x_1+\beta_2x_2+\beta_3x_1x_2+\epsilon$
		- $\beta_1+\beta_3x_2$
			- change in y for 1-unit increase in $x_1$
			- $x_1(\beta_1+\beta_3x2)$
		- $\beta_2+\beta_3x_1$
			- change in y for 1-unit increase in $x_2$
		- ![[Pasted image 20231126202901.png]]

---
# Reduced Models and the Extra SS F-test

- full model
	- includes all the parameters or predictor variables
- reduced model
	- hypotheses that some of the slopes of the predictor variables equal zero
	- should be taken out of the full model to make a reduced model

## Extra SS f-test
Also called Partial F-test or Nested F-test.

- $H_0:$ All selected beta's (slopes) equal 0
	- reduced
- $H_a:$ Not all selected beta's (slopes) equal 0
	- full

- Extra SS = SSE(reduced) - SSE(full)
	- SSE=$sum(observed-estimated)^2=\sum(x_i-\bar x)^2$
- Extra df = $df_{error}(reduced)-df_{error}(full)$
- $F=\frac{extraSS}{df_{error}(full)}\cdot\frac{SSE(full)}{extraDF}$

- $df=[extraDF,df_{error}(full)]$= (num of selected beta, n-(p+1))

---
# Building Models
- identify if the model has interactions