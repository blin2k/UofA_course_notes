# permutation matrix P
- orthogonal
	- $PP^T=P^TP=I$
	- $P^{-1}=P^T$
- one-hot

# Singularity and Non-Singularity
non-singularity matrix A
- inverse of A exists
	- $AA^{-1}=A^{-1}A=I$
- $det(A)\not=0$
- $rank(A)=n$
- for any vector $z\not=0$, $Az\not=0$

Basically, it means Linear Independence.

## Premultiply
When we have a linear system Ax=b, by premultiplying any nonsingular matrix M from the left, we can simplify the linear system without affection solution.
- MAx=Mb

- row scaling
	- premultiplying a nonsingular diagonal matrix D
		- DAx=Db
	- x is unchanged
- column scaling
	- postmultiplying A by D
		- ADx=b
	- rescales original solution
		- $x=(AD)^{-1}b=D^{-1}A^{-1}b$
	- retrieve the solution to the original system by premultiplying D

# Triangular Linear Systems
- what type of linear system is easy to solve?
	- only one entry in that row of a matrix is nonzero
		- solved by division
	- one more
		- substituting one known into it, then solved by division
	- pattern continues
- system with this property is called triangular
	- lower triangular
		- all entries above main diagonal are zero
	- upper triangular
		- all entries below main diagonal are zero

# Forward-substitution
For lower triangular system Lx=b,
$x_1=b_1/l_{11}$
- the first row is one-hot
$x_i=(b_i-\sum_{j=1}^{i-1}l_{ij}\cdot x_j)/l_{ii}$
- substitute then substract them, divide the current part

```python
for j=1 to n:
	if l_ij == 0:
		# stop if matrix is singular
		break
	x_j = b_j / l_jj
	for i=j+1 to n:
		b_i = b_i - l_ij * x_j
```

# Back-substitution
For upper triangular system Ux=b,
$x_n=b_n/u_{nn}$
$x_i=(b_i-\sum^b_{j=i+1}u_{ij}\cdot x_j)/u_{ii}$

```python
for j=n to 1:
	if u_jj=0:
		break
	x_j = b_j / u_jj
	for i=1 to j-1:
		b_i = b_i - u_ij * x_j
```

# Elimination
Transform general linear system into triangular form.

$$
\begin{bmatrix}
1&0\\
-a_2/a_1&1
\end{bmatrix}
\begin{bmatrix}
a_1\\a_2
\end{bmatrix}
=
\begin{bmatrix}
a_1\\0
\end{bmatrix}
$$
- manage to set the unwanted entry to be the opposite number
![[Pasted image 20240207190019.png]]
If you want to truncate at k, then for the kth column of M, set all entries after kth to be the pivot which can create a opposite number.

Also note that,
![[Pasted image 20240207190609.png]]
Therefore,
- $M_k=I-m_ke_k^T$
	- we have the ones and the opposite numbers
- $M_k^{-1}=I+m_ke_k^T$
	- $M_k^{-1}=L_k$ is the same as $M_k$ except the signs
- $M_kM_j=I-m_ke_k^T-m_je_j^T$
	- the mixed term is zero so this product becomes a union
![[Pasted image 20240207192241.png]]
- only modify the column that you want to truncate
	- I need to truncate at the first one
	- I modify the first column of the elimination matrix only
- the product of all elimination matrices is the union of them
	- it is easy to compute since we create EM column by column
- LL can be retrieved simply by reverse all of then signs excepts the diagonals

# Gaussian Elimination
- $M=M_{n-1}...M_1$
- $MAx=Mb$
- $U=MA$
	- $Ux=Mb$
	- back-substitution since we have U
![[Pasted image 20240207205107.png]]
That's why we can create a upper triangular.
# LU factorization
- $A=M^{-1}MA=M^{-1}U$
- $L=M^{-1}$ is a unit lower triangular matrix
	- $L=L_1L_2...$
- $A=LU$
	- $Ax=b\Rightarrow LUx=b$
		- $Ly=b$
		- $Ux=y$

```python
for k=1 to n-1:
	if a_kk == 0:
		break
	for i=k+1 to n:
		m_ik = a_ik/a_kk
	for j=k+1 to n:
		a_ij = a_ij - m_ik * a_kj
```

>[!notice]
>Inversion gives less accurate answer
>e.g. $3^{-1}\approx 0.333$
>Matrix inversion often occur as notation but rarely in implementation

# Geometric Interpretation of Singularity
In 2D
- solution is intersection point of two straight lines
- if lines are not parallel
	- nonsingular
	- solution is unique
- if lines are parallel
	- singular
	- no interaction or coincide
		- no solution or any point along the line is solution

If matrix A is singular and there are solutions
![[Pasted image 20240207222143.png]]
- for any solution y, y+gamma\*z is also a solution
	- gamma is any real number
	- Az = 0