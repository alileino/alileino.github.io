---
layout: post
title: Proofs for the perceptron learning algorithm (WIP)
---

$$\newcommand{\sign}{\textrm{sign}}
\newcommand{\norm}[1]{\|#1\|}
$$

# Definitions
Let $t\in\mathbb{N}$ be the time step, $w(t)\in\mathbb{R}^n$ the weight vector at time $t$, and $(x(t), y(t))$ any misclassified pair misclassified at time $t$.
The perceptron learning algorithm learning rule using this notation is:

<div class="result">
$$ \begin{equation}
w(t+1) = w(t) + y(t)x(t)
\end{equation}$$
</div>
and its classification rule is

<div class="result">
$$
\begin{equation}
h(x) = \sign(w^Tx)
\end{equation}
$$
</div>

For any misclassified pair $x(t), y(t)$, we have 

<div class="result">
$$
\begin{equation}
\sign(w^T(t)x(t))=-\sign(y(t))=-y(t)
\label{eq:misclass} 
\end{equation}
$$
</div>
# Proofs
<div class="result">
$$
\begin{equation}
y(t)w^T(t)x(t) < 0
\label{eq:misclass_lt}
\end{equation}
$$
</div>

<div class="proof">
$$
\begin{align*}
&\sign(y(t)w^T(t)x(t))\\
&=\sign(y(t))\sign(w^T(t)x(t)) & & & \vert y(t) \textrm{ is misclassified by } w(t)\\
&\stackrel{\eqref{eq:misclass}}{=}\sign(y(t))(-\sign(y(t))\\
&=-y(t)^2\\
&=-1
\end{align*}
$$
</div>
<div class="result">
$$
\begin{equation}
y(t)w^T(t+1)x(t)>y(t)w^Tx(t)
\label{eq:improvement}
\end{equation}
$$
</div>
<div class="proof">

$$ 
\begin{align*}
&y(t)w^T(t+1)x(t) \\
&= y(t)(w(t)+y(t)x(t))^Tx(t)\\
&=y(t)(w^T(t)+x^T(t)y(t))x(t)\\
&=y(t)w^T(t)x(t)+y(t)^2 x(t)^2\\
&>y(t)w^T(t)x(t)
\end{align*}
$$
</div>
Where $y(t)^2x(t)^2>0$, since $x$ includes the bias dimension, so it can't be $0$. The main takeaway of equation \eqref{eq:improvement} is that the RHS is guaranteed to be less than 0 because $x(t)$ is misclassified, but the LHS is strictly greater than RHS which means that it may become greater than 0 after the update. If LHS becomes greater than 0, then the point $x(t)$ would be correctly classified by $w(t+1)$. However, equation \eqref{eq:improvement} does not guarantee that $w(t+1)$ correctly classifies $x(t)$, it only guarantees improvement in the value of $w^T(t+1)x(t)$ over $w^T(t)x(t)$ in the direction of $y(t)$.

## Convergence for linearly separable data
We assume the design matrix $X=\[x_1,x_2, \dots, x_N\]$ is linearly separable. Let $w^*$ be an optimal set of weights separating the data. For simplicity we assume $w(0)=0$

For all $i, w^* $ 
correctly classifies $x_i$. Then $y_i=\sign({w^*}^T x_i)$ 
<div class="result">
$$
\begin{equation}
\rho=\min_{1\leq i\leq N} y_i({w^*}^Tx_i)) > 0
\end{equation}
$$
</div>
<div class="proof">
$$
\begin{align*}
\sign(\rho) &= \sign(\min_{1\leq i\leq N} y_i({w^*}^Tx_i))\\
&=\sign(y_m({w^*}^Tx_m))\\
&=\sign(y_m)^2\\
&= 1 > 0\\
\end{align*}
$$
</div>
<div class="result">
$$
\begin{equation}
w^T(t)w^*=w^T(t-1)w^*+\rho
\end{equation}
$$
</div>
<div class="proof">
$$
\begin{align*}
w^T(t)w^* &= w^T(t-1)w^*+\rho\\
&= (w(t-1)+y(t-1)x(t-1))^Tw^*\\
&= w^T(t-1)w^*+y(t-1)x^T(t-1)w^*\\
&= w^T(t-1)w^*+(y(t-1)w^{*T}x(t-1))^T \\
&\geq w^T(t-1)w^*+\rho \\
\end{align*}
$$
</div>
<div class="result">
$$
\begin{equation} w^T(t)w^* \geq t\rho
\label{eq:bound_on_weight_mul}
\end{equation}
$$
</div>
<div class="proof">

$w^T(0)w^* =0\rho$ so the base case holds. By induction we get $w^T(t)w^* \geq w^T(t-1)w^*+\rho \geq (t-1)\rho + \rho = t\rho$
</div>

<div class="result">
$$
\begin{equation}
\norm{w(t)}^2 \leq \norm{w(t-1)}^2+\norm{x(t-1)}^2
\end{equation}
$$
</div>
<div class="proof">
$$
\begin{align*}
\norm{w(t)}^2 &= \norm{w(t-1)+y(t-1)x(t-1)}^2 \\
&=\norm{w(t-1)}^2 + 2y(t-1)w^T(t-1)x(t-1) + \norm{y(t-1)x(t-1)}^2 \\
&=\norm{w(t-1)}^2 + 2y(t-1)w^T(t-1)x(t-1) + \norm{x(t-1)}^2\\
&\stackrel{\eqref{eq:misclass_lt}}{\leq} \norm{w(t-1)}^2 + \norm{x(t-1)}^2 
\end{align*}
$$
</div>
<div class="result">
$$
\begin{equation}
\norm{w(t)}^2 \leq tR^2 \textrm{, where } R=\max_{1\leq i \leq N} \norm{x_i}
\label{eq:wt_lt_tr}
\end{equation}
$$
</div>

<div class="proof">
It follows from the definition of $R$ that $R^2 \geq \norm{x_i}^2$ for any $i$. $\norm{w(0)}^2 = 0\cdot R^2$, so the base case holds. Let $t>0$. Then $\norm{w(t)}^2 \leq \norm{w(t-1)}^2 + \norm{x(t-1)}^2 \leq (t-1)R^2 + R^2 = tR^2$.
</div>

<div class="result">
$$
\begin{equation}
t \leq \frac{R^2\norm{w^*}^2}{\rho^2}
\end{equation}
$$

</div>
<div class="proof">

$$
\begin{align*}
\frac{w^T(t)w^*}{\norm{w(t)}} &\stackrel{\eqref{eq:bound_on_weight_mul}}{\geq}
\frac{t\rho}{\norm{w(t)}}\\
&\stackrel{\eqref{eq:wt_lt_tr}}{\geq}
\frac{t\rho}{\sqrt{t}R} = \frac{\sqrt{t}}{R}
\end{align*}
$$

$$
\begin{align*}
\Rightarrow \sqrt{t} &\leq \frac{w^T(t)w^* R}{\norm{w(t)}\rho}\\
\Rightarrow t &\leq \frac{(w^Tw^*)(w^Tw^*)R^2}{\norm{w(t)}^2\rho^2}\\
&= \frac{\norm{w(t)}^2\norm{w^*}^2R^2}{\norm{w(t)}^2\rho^2}\\
&=\frac{\norm{w^*}^2R^2}{\rho^2}
\end{align*}
$$
</div>
The last result means that there is an upper bound for $t$ (number of iterations) given a linearly separable data set. One interpretation of this is that if $t$ were larger than the bound, there would be no misclassified examples and the update rule would not apply.

TBC
<!-- Try these? http://drz.ac/2013/01/17/latex-theorem-like-environments-for-the-web/ -->