# Zero-Sum Games
- gains and loses are perfectly balanced
- $U_i=-U_{-i}$
	- the winner gains the same amount of what the loser lost

# Minimax Search
Since we can calculate the utility for one player given another one, we only need to state one on the tree.

![[Pasted image 20240417180750.png]]
- one wants to maximize the value while another one wants to minimize it
- still $O(b^d)$
# Alpha-Beta Pruning
![[Pasted image 20240417181931.png]]
Player 2 is trying to minimize the value. When player 2 chose a value lower than the current root, there is no need to check other terminals in the subtree because it can only go down and player 1 has no interests in how down it is.

Alpha is the root value when it is trying to maximize, Beta is the opposite.

def AlphaBeta(n, alpha, beta):
	if n in Z:
		return u(n)
	M = inf if P(n) = Max else -inf
	for a in A(n):
		if P(n) = Min:
			M = min(M, AlphaBeta(T(n,a), alpha, beta))
			if M <= alpha:
				return M
			beta = min(M, beta)
		if P(n) = Max:
			M = max(M, AlphaBeta(T(n,a), alpha, beta))
			if M >= beta:
				return M
			alpha = max(M, alpha)
	return M
- if the current one is a terminal, return the value
- else, initialize the guess as inf or -inf
	- for each child, check if the child is better than the current one
		- using min()
	- alpha is passed from the last layer, if the current one is smaller than alpha, then the current one can only go down, thus we can pruned it by return it
	- update beta if not pruned
![[Pasted image 20240417185218.png]]
As the 3 is updated, the 2 subtrees can be pruned.
![[Pasted image 20240417190218.png]]
- $O(b^{d/2})$
![[Pasted image 20240417191020.png]]

# Limited Resources
- search tree is too large for BI and AB
	- chess
- iterative deepening search
	- evaluate the leaf nodes with a heuristic function
		- heuristic function should be fast and accurate

The evaluation function should approximate the right order.
- the value doesn't matter