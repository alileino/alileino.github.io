---
layout: post
title: Proofs for the perceptron learning algorithm (WIP)
---
$$\newcommand{\sign}{\textrm{sign}}$$
# Definitions
Let $t\in\mathbb{N}$ be the time step, $w(t)\in\mathbb{R}^n$ the weight vector at time $t$, and $(x(t), y(t))$ any misclassified pair misclassified at time $t$.
The perceptron learning algorithm learning rule using this notation is:

$$ \begin{equation}
w(t+1) = w(t) + y(t)x(t)
\end{equation}$$

and its classification rule is

$$
\begin{equation}
h(x) = \sign(w^Tx)
\end{equation}
$$

For any misclassified pair $x(t), y(t)$, we have 

$$
\begin{equation}
\sign(w^T(t)x(t))=-\sign(y(t))=-y(t)
\label{eq:misclass} 
\end{equation}
$$

# Proofs

$$
\begin{equation}
y(t)w^T(t)x(t) < 0
\end{equation}
$$

__Proof:__

$$
\begin{align*}
&\sign(y(t)w^T(t)x(t))\\
&=\sign(y(t))\sign(w^T(t)x(t)) & & & \vert y(t) \textrm{ is misclassified by } w(t)\\
&\stackrel{\eqref{eq:misclass}}{=}\sign(y(t))(-\sign(y(t))\\
&=-y(t)^2\\
&=-1
\end{align*}
$$

$$
\begin{equation}
y(t)w^T(t+1)x(t)>y(t)w^Tx(t)
\label{eq:improvement}
\end{equation}
$$

__Proof:__ 

$$ 
\begin{align*}
&y(t)w^T(t+1)x(t) \\
&= y(t)(w(t)+y(t)x(t))^Tx(t)\\
&=y(t)(w^T(t)+x^T(t)y(t))x(t)\\
&=y(t)w^T(t)x(t)+y(t)^2 x(t)^2\\
&>y(t)w^T(t)x(t)
\end{align*}
$$

Where $y(t)^2x(t)^2>0$, since $x$ includes the bias dimension, so it can't be $0$. The main takeaway of equation \eqref{eq:improvement} is that the RHS is guaranteed to be less than 0 because $x(t)$ is misclassified, but the LHS is strictly greater than RHS which means that it may become greater than 0 after the update. If LHS becomes greater than 0, then the point $x(t)$ would be correctly classified by $w(t+1)$. However, equation \eqref{eq:improvement} does not guarantee that $w(t+1)$ correctly classifies $x(t)$, it only guarantees improvement in the value of $w^T(t+1)x(t)$ over $w^T(t)x(t)$ in the direction of $y(t)$.

## Convergence for linearly separable data
Assume the design matrix $X=\[x_1,x_2, \dots, x_N\]$ is linearly separable. Let $w^*$ be an optimal set of weights separating the data.

For all $i, w^* $ 
correctly classifies $x_i$. Then $y_i=\sign({w^*}^T x_i)$ 

$$\rho=\min_{1\leq i\leq N} y_i({w^*}^Tx_i)) > 0$$

__Proof:__

$$
\begin{align*}
\sign(\rho) &= \sign(\min_{1\leq i\leq N} y_i({w^*}^Tx_i))\\
&=\sign(y_m({w^*}^Tx_m))\\
&=\sign(y_m)^2\\
&= 1 > 0\\
\end{align*}
$$

TBC