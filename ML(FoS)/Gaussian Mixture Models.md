- mixture of Gaussian
	- $x|t=k\sim \mathcal N(\mu_k,\sum_k)$
		- t - type
		- x - features
		- $\sum$ - co-variance
	- $t\sim Categorical(\pi_1,...,\pi_k)$
		- $P(t=k)=\pi_k$
	- each label is normal distributed but the whole sample distribution may not
			- in a zoo, the weight-size distribution of a specific species is normal distributed, but that of all animals in the zoo may not. the latter may have multiple peaks

$$\begin{align}
lg(P(D))&=\sum lg[P(t^m)\cdot P(x^m|t^m)]\\
&=\sum lg(P(t^m))+\sum lg(P(x^m|t^m))
\end{align}$$
- the 1st term only contains $\pi_k$
- the 2nd term only contains $\mu_k,\sum_k$
	- $=\sum_k\sum_{m:t^m=k}lg(P(x^m|t^m=k))$
		- separate into different categories k
		- each category only cares about its own $\mu,\sum$
	- $=\sum_k\sum_m\mathbb 1\{t^m=k\}\cdot lg(P(x^m|t^m))$
		- for each category, go through the whole dataset and only care about the samples in the current category  

$\hat \pi_k=\frac{\sum_m\mathbb 1\{t^m=k\}}{M}$
- the probability of having this category over the dataset
- counting 

$\hat \mu_k=\frac{\sum_m\mathbb 1\{t^m=k\}\cdot x^m}{\sum_m\mathbb 1\{t^m=k\}}$
- the sum of samples in this category divided by the number of samples in this category
	- the average (mean)
- the indicator function is just a filter

$\hat \sum_k=\frac{\sum_m\mathbb 1\{t^m=k\}\cdot(x^m-\mu_k)(x^m-\mu_k)^T}{\sum_m\mathbb 1\{t^m=k\}}$
- average error square
	- $SE^2=var$
- Gaussian co-variance estimation


$P(x,t=i)$
$\rightarrow P(t=i)P(x|t=i)$
$\rightarrow \pi_i\cdot C_i\cdot exp\{-\frac12(x-\mu_i)^T\sum_i^{-1}(x-\mu_i)\}$
- the co-variance is the denominator in the Gaussian distribution


Comparing probabilities of each label, we choose the highest one.
- if the co-variance are the same, the decision boundary is linear
	- log both side, you get what is inside the exp plus pi and a constant
- otherwise, it is quadratic