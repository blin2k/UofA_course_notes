Supervised Learning
- Stage 1: Training / Learning
	- input -> output
		- computer readable input: e.g. image -> pixels -> vector representation / coordinate
		- "categorical -> index" is not a good approach, feature matrix(vector) performs better. e.g. $\begin{bmatrix}x_{1}\\ x_2\\ x_3\end{bmatrix}$ x1: about oil industry, x2: education, x3: healthcare
	- learn a function: $\mathbb R^d\rightarrow \mathbb R$ 
		- task: the output should be ==a single number==
		- demanding for multi-task could be done by doing multiple single tasks one by one
- Stage 2: Inference / Prediction
	- $x_* \rightarrow \hat y_*$ where $x_*\in \mathbb R^d$

	We don't call the stage 2 testing because it sounds like you know the answer beforehand.

> [!notice]
> - For simplicity, we're going to focus on fixed-dimensional real features.
> - We're not focusing on feature design.

1. Humans specify a restricted class $\mathbb H\subset \{h:\mathbb R^d\rightarrow\mathbb R\}$, which the ML system can pick $h$ from. We rule out some functions manually. 
	- "Inductive bias" is what keep the output from overfitting, and allowing the output function to predict the future. 
	- $\mathbb H$: hypothesis class
	- $h$ : a hypothesis
2. Humans specify a loss function (preference)
	- e.g. $\mathbb J(h,\mathbb D_{train})$
	- $\frac12\sum^{(M)}_{n=1}|h(x^{(m)})-y^{(m)}|^2$
3. Machine minimizes the loss function
	- minimizing $h\in\mathbb H$ from $\mathbb J(h,\mathbb D_{train})$

4. Evaluate the ML model
	- define a measure of success $E(h,\{x_*^{(m)}\}^{(M')}_{m=1},\{y_*^{(m)}\}^{(M')}_{m=1})$ (e.g. Accuracy, absolute gain / loss) depends on the task
