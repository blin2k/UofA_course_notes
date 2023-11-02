# Relationship Among Hyperparameters

- $||w||^2\le C$
	- if C is large
		- considering lots of $w$
		- to tone it
			- set the shrinkage parameter $\lambda$ smaller
		- but still a complex model 
			- large H
				- low bias
				- high variance $\sigma_\epsilon$
				- overfitting

## Example
If we have a ==prior uniform==
- $P(w)= C$ for every w and $C\not=0$
- improper prior
	- unbounded
	- not integrated to 1
 
In this case, MLE is the same as MAP because the P(w) is a constant which can be wiped out when we are considering argmax. 

In other word, the penalized term is gone.

You know the graph is flat, which is close to a high variance graph rather than a small variance one.

That is the same as what happened when the shrinkage parameter is small since it scales the penalized term.

Therefore, when the constrain of w is weak, the variance will be high. 

---
How can we choose $C/\lambda/\sigma_w$?
	We only choose one of them because they response to each other. 
- tuning $\lambda$ is easy

HOW?
- optimize $\lambda$ during ML training
	- $\underset{w,\lambda}{minimize}\quad \frac1{2M}||Xw-t||^2+\lambda||w||^2$
		- $\lambda$ unavoidably goes to 0
		- not gonna work
- try different predefined values of $\lambda$
	- for each value, train the model on $D_{train}$ and test it on $D_{test}$, return the one with the lowest test error
		- expensive, and sometimes the access to $D_{test}$ is limited
		- possible but not practical and problematic
		- since it goes through the test set multiple times, it might overfitting the test set
	- create a fake test set named $D_{val}$ by separating a portion of the training set
		- only access the true test set once
			- training: $w_\lambda=\underset w{argmin}\quad J_\lambda(w,D_{train})$
			- validation: $Err_\lambda=Err(w_\lambda,D_{val})$
			- $\lambda^*=\underset\lambda{argmin}\quad Err_\lambda$

On what value?
- single hyperparameter
	- 0.01 -> 0.03 -> 0.1 -> 0.3 ->...
- a few hyperparameters
	- trying every combination
		- expensive
	- grid search, coordinate decent
		- set the rest fixed and train the chosen one, then switch the table and train the previously fixed one
		- recursively doing this, the values will converge 
- lots of hyperparameters
	- expertise