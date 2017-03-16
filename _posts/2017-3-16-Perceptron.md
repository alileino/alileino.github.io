---
layout: post
title: Proofs for the perceptron learning algorithm
---
$$\newcommand{\sign}{\textrm{sign}}$$

Let $t\in\mathbb{N}$ be the time step, $w(t)$ the weight vector at time $t$, and $x(t), y(t)$ any misclassified pair misclassified at time $t$.
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
\tag{213}
\end{equation}$$.


$$
\begin{equation}
y(t)w^T(t)x(t) < 0
\end{equation}
$$

Proof: $$
\begin{align*}
&\sign(y(t)w^T(t)x(t))\\
&=\sign(y(t))\sign(w^T(t)x(t)) & & & \vert y(t) \textrm{ is misclassified by } w(t)\\
&\stackrel{\ref{eq:misclass}}{=}\sign(y(t))(-\sign(y(t))\\
&=-\sign(y(t))^2\\
&=-1
\end{align*}
$$\ref{eq:misclass}
\eqref{eq:misclass}
\eqref{misclass}

$$
\begin{equation}
y(t)w^T(t+1)x(t)>y(t)w^Tx(t)
\end{equation}
$$
Proof: $$ 
\begin{align*}
&y(t)w^T(t+1)x(t) \\
&= y(t)(w(t)+y(t)x(t))^Tx(t)\\
&=y(t)(w^T(t)+x^T(t)y(t))x(t)\\
\end{align*}
$$
