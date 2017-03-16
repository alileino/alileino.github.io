---
layout: post
title: Proofs for the perceptron learning algorithm
---
$$\newcommand{\sign}{\textrm{sign}}$$

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

Clearly for any misclassified pair $x(t), y(t)$, we have 

$$
\begin{equation}
\sign(w^T(t)x(t))=-\sign(y(t))
\label{eq:misclass} 
\end{equation}
$$.

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
&=-\sign(y(t))^2\\
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

Where $y(t)^2x(t)^2>0$, since $x$ includes the bias dimension, so it can't be $0$. The main takeaway of equation \eqref{eq:improvement} is that the RHS is guaranteed to be less than 0 because $x(t)$ is misclassified, but the LHS is strictly greater than RHS which means that it may at some point be greater than 0. At that point $x(t)$ would be correctly classified by $w(t+1)$. This is not guaranteed by \eqref{eq:improvement} however, only the improvement over the previous classification.

