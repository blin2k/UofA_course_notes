# Extensive-Form Game
![[Pasted image 20240417171825.png]]
- like chess, players take turns to move

![[Pasted image 20240417172251.png]]

def BI(n):
	if  n in Z:
		return u(n)
	B = \[-inf. -inf, ...]
	for a in A(n):
		v = BI(T(n,a))
		if v\[P(n)] > B\[P(n)]
			B = v
	return B

- Z
	- terminal states
- B
	- utility profile

![[Pasted image 20240417174439.png]]
- if not hit the terminal, keep going
- if hit, record the utility list and go backward
	- when backing, check whose turn is it, then update the child with better utility for the current player

Since it is going to reach all terminals, the complexity will be $O(b^d)$
