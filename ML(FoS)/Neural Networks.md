Non-linearity
- manually designed non-linear features
- kernels
	- use manually designed inner-product to summarize non-linear features
	- manually designed things may harm the model
- neural networks
	- learns (probably) non-linear features automatically

---
Motivation: A simple non-linear classification XOR
- (1,0) and (0,1) is a true XOR
	- 1
- (0,0) and (1,1) is not
	- 0

	This cannot be solve perfectly by linear classification. But can be solved by stacking multiple linear classifiers.

The result can be shown in a new coordinate
![[Pasted image 20231130043028.png]] 

Now we can use a new linear classifier to cut c2c3 out.