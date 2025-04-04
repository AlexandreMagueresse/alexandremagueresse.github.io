+++
title = "ODE integrators"
hasmath = true
hascode = false
date = Date(2025, 03, 31)

rss_title = "ODE integrators"
rss_description = "ODE integrators"
rss_pubdate = Date(2025, 03, 31)

tags = ["research"]
+++

\backtonotes

# General framework

We consider the initial value problem
$$\mb{u}(t_{0}) = \mb{u}_{0}, \qquad \mb{r}(t, \mb{u}, \dot{\mb{u}}) = \mb{0},$$
where
* $\mb{u}: \RR \to \RR^{n}$ is the unknown of the problem,
* $t_{0} \in \RR$ is the initial time and $\mb{u}_{0} \in \RR^{n}$ is the initial condition,
* $\mb{r}: \RR \times \RR^{n} \times \RR^{n} \to \RR^{n}$ is a discretised residual operator.
We are willing to evolve $\mb{u}$ until $t_{F} > t_{0}$. We split the interval $\cc{t_{0}}{t_{F}}$ into sub-intervals $\cc{t_{n}}{t_{n+1}}$ and evolve the solution from $t_{n}$ to $t_{n+1}$ iteratively. More formally, we consider the following general framework:
* The **encoder map** $\mc{E}: \RR^{n} \to \mc{S}$ embeds the initial condition into a state space $\mc{S}$,
* The **update map** $\mc{U}: \RR_{+} \times \mc{S} \to \mc{S}$ evolves the state during one time interval $\cc{t_{n}}{t_{n+1}}$,
* The **decoder map** $\mc{D}: \mc{S} \to \RR^{n}$ converts the state into the value of $\mb{u}$.
We then consider the recurrence
$$\mb{s}_{0} = \mc{E}(\mb{u}_{0}), \qquad \mb{s}_{n+1} = \mc{U}(h_{n}, \mb{s}_{n}), \qquad \mb{u}_{n} = \mc{D}(\mb{s}_{n}),$$
where $h_{n} = t_{n+1} - t_{n}$. We want to design $(\mc{E}, \mc{U}, \mc{D})$ so that $\mb{u}_{n}$ is a good approximation of $\mb{u}(t_{n})$. In particular, note that at time $t_{0}$ we must have $\mc{D} \circ \mc{E}(\mb{u}_{0}) = \mb{u}_{0}$; in other words, $\mc{D} \circ \mc{E} = \operatorname{Id}_{\RR^{n}}$.

A scheme is **consistent** if the local truncation error goes to zero with the step size, where the local truncation error is defined as $\mb{u}_{n+1} - \mb{u}(t_{n+1})$ assuming that $\mb{u}_{n} = \mb{u}(t_{n})$. A scheme has **order** $p$ if $\mb{u}_{n+1} - \mb{u}(t_{n+1}) = \mc{O}(h_{n}^{p+1})$.

The **region of absolute stability** is the set of all complex $z = \lambda h$ such that when evolving the linear ODE $\mb{r}(t, \mb{u}, \dot{\mb{u}}) = \dot{\mb{u}} - \lambda \mb{u}$, the numerical solution tends to $\mb{0}$ when time goes to infinity. A scheme is **A-stable** if its region of absolute stability contains the entire left complex plane. A scheme is **L-stable** if it is A-stable and if the rate at which $\mb{u}_{n}$ goes to $\mb{0}$ increases as $\Re(\lambda) \to -\infty$. In the case of a linear scheme, one can identify an amplification matrix $\mc{A}(z): \mc{S} \to \mc{S}$. The stability of the scheme directly depends on the eigenvalues of $\mc{A}(z)$.

# $\theta$-method
The $\theta$ method consists in enforcing a zero residual at $t_{n + \theta} = (1 - \theta) t_{n} + \theta t_{n+1}$. More precisely, find $\mb{v} \in \RR^{n}$ such that
$$\mb{r}(t_{n+\theta}, \mb{u}_{n} + \theta h_{n} \mb{v}, \mb{v}) = \mb{0}$$
and set $\mb{u}_{n+1} = \mb{u}_{n} + h_{n} \mb{v}$. Assume that $\mb{r}(t, \mb{u}, \dot{\mb{u}}) = \dot{\mb{u}} - f(t, \mb{u})$. The third-order Taylor expansion of the exact solution is
$$\begin{align*}
\mb{u}(t_{n+1}) &= \mb{u}(t_{n}) + h_{n} \dot{\mb{u}}(t_{n}) + \frac{1}{2} h_{n}^{2} \ddot{\mb{u}}(t_{n}) + \mc{O}(h_{n}^{3}) \\
&= \mb{u}(t_{n}) + h_{n} f(t_{n}, \mb{u}_{n}) + \frac{1}{2} h_{n}^{2} (\partial_{t} f(t_{n}, \mb{u}_{n}) + \partial_{\mb{u}} f(t_{n}, \mb{u}_{n}) f(t_{n}, \mb{u}_{n})) + \mc{O}(h_{n}^{3}).
\end{align*}$$
The third-order Taylor expansion of the numerical solution is
$$\begin{align*}
\mb{u}_{n+1} &= \mb{u}_{n} + h_{n} f(t_{n} + \theta h_{n}, \mb{u}_{n} + \theta h_{n} \mb{v}) \\
&= \mb{u}_{n} + h_{n} f(t_{n}, \mb{u}_{n}) + \theta h_{n}^{2} \partial_{\mb{u}} f(t_{n}, \mb{u}_{n}) \mb{v} + \theta h_{n}^{2} \partial_{t} f(t_{n}, \mb{u}_{n}) + \mc{O}(h_{n}^{3}) \\
&= \mb{u}_{n} + h_{n} f(t_{n}, \mb{u}_{n}) + \theta h_{n}^{2} \partial_{\mb{u}} f(t_{n}, \mb{u}_{n}) f(t_{n}, \mb{u}_{n}) + \theta h_{n}^{2} \partial_{t} f(t_{n}, \mb{u}_{n}) + \mc{O}(h_{n}^{3}).
\end{align*}$$
Observe that regardless of $\theta$, the expansions $\mb{u}(t_{n+1})$ and $\mb{u}_{n+1}$ coincide up to $\mc{O}(h_{n})$, so the $\theta$-method is at least of order $1$. They coincide up to $\mc{O}(h_{n})$ if and only if $\theta = 1/2$.

In the case of a linear first-order ODE, one readily finds $\mb{v} = \lambda (1 - \theta z)^{-1} \mb{u}_{n}$, and
$$\mc{A}(z) = 1 + \frac{z}{1 - \theta z}.$$
Observe that
$$\abs{\mc{A}(z)} \leq 1 \iff (1 - 2 \theta) \abs{z}^{2} + 2 \Re(z) \leq 0.$$
We distinguish three classes:
* If $\theta < 1/2$, the stability region is the circle of radius $1 / (1 - 2 \theta)$ centred at $(-1/(1 - 2 \theta), 0)$. This scheme is not $A$-stable. The case $\theta = 0$ is known as Forward Euler and it is the only explicit scheme of the family.
* If $\theta = 1/2$, the stability region is the whole left complex plane. The scheme is $A$-stable. It is known as the implicit midpoint scheme.
* If $\theta > 1/2$, the stability region includes the whole complex plane except the circle of radius $1 / (2 \theta - 1)$ and centred at $(1 /(2 \theta - 1), 0)$. In particular, this scheme is $A$-stable. The special case $\theta = 1$ is known as Backward Euler.
The scheme is only $L$-stable when $\theta = 1$.

# Runge-Kutta

The Runge-Kutta method is a multi-stage method consisting in enforcing a zero residual at intermediate times between $t_{n}$ and $t_{n+1}$, and forming $\mb{u}_{n+1}$ from linear combinations of these intermediate solutions. More precisely, given $s \geq 1$, $\mb{c} \in \RR^{s}$, $\mb{A} \in \RR^{s \times s}$ and $\mb{b} \in \RR^{s}$, find $(\mb{v}_{1}, \ldots, \mb{v}_{s})$ such that
$$\mb{r}(t_{n} + \mb{c}_{i} h_{n}, \mb{u}_{n} + h_{n} \sum_{j = 1}^{s} \mb{A}_{ij} \mb{v}_{j}, \mb{v}_{i}) = \mb{0}$$
for all $i \in \{1, \ldots, s\}$ and finally set
$$\mb{u}_{n+1} = \mb{u}_{n} + h_{n} \sum_{i = 1}^{s} \mb{b}_{i} \mb{v}_{i}.$$
A Runge-Kutta is thus entirely determined from the coefficients $\mb{A}$, $\mb{b}$ and $\mb{c}$. They are conveniently arranged in the Butcher tableau format
$$\begin{array}{c|c}
\mb{c} & \mb{A} \\
\hline
& \mb{b}^{\ast}
\end{array}.$$

Applied to a linear ODE with constant step size $h$, letting $\mb{v} = (\mb{v}_{1}, \ldots, \mb{v}_{s}) \in \RR^{s}$, this recursion becomes
$$\mb{v} = \lambda (\mb{1}_{s} \mb{u}_{n} + h \mb{A} \mb{v}), \qquad \mb{u}_{n+1} = \mb{u}_{n} + h \mb{b}^{\ast} \mb{v}.$$
We infer $\mb{v} = \lambda (\mb{I} - z \mb{A})^{-1} \mb{1}_{s} \mb{u}_{n}$ and $\mb{u}_{n+1} = (1 + z \mb{b}^{\ast} (\mb{I} - z \mb{A})^{-1} \mb{1}) \mb{u}_{n}$, that is
$$\mc{A}(z) = 1 + z \mb{b}^{\ast} (\mb{I} - z \mb{A})^{-1} \mb{1}.$$
The order conditions for order $p$ are found by enforcing $\mb{c} = \mb{A} \mb{1}$ and looking at the rooted trees of size $\leq p$. In the following expressions, summation is understood for all appearing variables, in the range $\{1, \ldots, s\}$.
* **Order 1** $b_{i} = 1$.
* **Order 2** $b_{i} c_{i} = 1/2$.
* **Order 3** $b_{i} c_{i}^{2} = 1/3$, and $b_{i} A_{ij} c_{j} = 1/6$.
* **Order 4** $b_{i} A_{ij} A_{jk} c_{k} = 1/24$, $b_{i} A_{ij} c_{j}^{2} = 1/12$, $b_{i} c_{i} A_{ij} c_{j} = 1/8$ and $b_{i} c_{i}^{3} = 1/4$.
In the following, we look at one- and two-stage schemes and satisfy the order conditions one by one until possible.

## 1 stage
A generic one-stage, first-order RK scheme looks like
$$\begin{array}{c|c}
\alpha & \alpha \\ \hline
& 1
\end{array},$$
for some $\alpha \in \RR$ (usually $\alpha \in [0, 1]$). This is precisely the $\theta$-scheme presented above.

This scheme has order $2$ when $\alpha = 1/2$; it is the implicit midpoint rule corresponding to $\theta = 1/2$ in the $\theta$-scheme. Neither of the conditions for order $3$ are satisfied.

## 2 stages
A generic two-stage, first-order RK scheme looks like
$$\begin{array}{c|cc}
\alpha & \bar{\alpha} & \alpha - \bar{\alpha} \\
\beta & \beta - \bar{\beta} & \bar{\beta} \\ \hline
& \gamma & 1 - \gamma
\end{array},$$
where $\alpha, \bar{\alpha}, \beta, \bar{\beta}, \gamma \in \RR$. There is a lot of freedom in these choices so one generally only considers two-stage RK schemes of order $2$.

The second-order conditions are satisfied when $\gamma \alpha + (1 - \gamma) \beta = 1/2$, that is for the two classes
$$\begin{array}{c|cc}
1/2 & \bar{\alpha} & 1/2 - \bar{\alpha} \\
1/2 & 1/2 - \bar{\beta} & \bar{\beta} \\ \hline
& \gamma & 1 - \gamma
\end{array}, \qquad \text{or} \qquad
\begin{array}{c|cc}
\alpha & \bar{\alpha} & \alpha - \bar{\alpha} \\
\beta & \beta - \bar{\beta} & \bar{\beta} \\ \hline
& \frac{\beta - 1/2}{\beta - \alpha} & \frac{1/2 - \alpha}{\beta - \alpha}
\end{array},$$
for some $\beta \neq \alpha$. We now look at these two classes separately.

### First class
Note that this scheme reduces to a one-stage method when $\bar{\alpha} + \bar{\beta} = 1/2$.
$$\begin{array}{c|cc}
1/2 & \bar{\alpha} & 1/2 - \bar{\alpha} \\
1/2 & 1/2 - \bar{\beta} & \bar{\beta} \\ \hline
& \gamma & 1 - \gamma
\end{array}$$
The stability function is
$$\mc{A}(z) = \frac{1 + z/2 - v z^{2}}{1 - z/2 + v z^{2}}, \qquad v = \alpha \beta - \bar{\alpha} \beta - \alpha \bar{\beta}.$$
If $v = 0$, the scheme is A-stable. Otherwise, the stability region is the hyperbola $(x - w)^{2} - y^{2} \geq w^{2}$, where $w = 1 / (4 v)$. The scheme is never L-stable.

Neither of the conditions for order $3$ can be met.

### Second class
A family of explicit two-stage, second-order RK schemes is as follows
$$\begin{array}{c|cc}
0 & 0 & 0 \\
\alpha & \alpha & 0 \\ \hline
& 1 - \frac{1}{2 \alpha} & \frac{1}{2 \alpha}
\end{array}.$$
The stability function is $\mc{A}(z) = 1 + z / 2$. Choosing $\alpha = 1$ yields Heun's method (also known as improved Euler or explicit trapezoidal rule). The choice $\alpha = 2/3$ is known as Ralston's method and minimises the local truncation error. Choosing $\alpha = 1/2$ provides the explicit midpoint rule, which is a predictor-corrector scheme.

Among the diagonally-implicit methods
$$\begin{array}{c|cc}
\alpha & \alpha & 0 \\
\beta & \beta - \bar{\beta} & \bar{\beta} \\ \hline
& \frac{\beta - 1/2}{\beta - \alpha} & \frac{1/2 - \alpha}{\beta - \alpha}
\end{array},$$
Crank-Nicolson is the most popular and corresponds to $\alpha = \bar{\alpha} = 1/2$, $\beta = \bar{\beta} = 1/2$. More generally, the stability function is
$$\mc{A}(z) = \frac{1 + (1/2 - \alpha - \bar{\beta}) z}{1 - (\alpha + \beta) z + \alpha \beta z^{2}}.$$
The stability region is difficult to analyse, but this scheme may only be L-stable when $\alpha \beta \neq 0$ or when $\alpha \beta = 0$, $\alpha + \beta \neq 0$ and $\bar{\beta} = 1/2 - \alpha$. The singly-diagonally-implicit constraint helps simplify the analysis
$$\begin{array}{c|cc}
\alpha & \alpha & 0 \\
\beta & \beta - \alpha & \alpha \\ \hline
& \frac{\beta - 1/2}{\beta - \alpha} & \frac{1/2 - \alpha}{\beta - \alpha}
\end{array}.$$
The two most famous choices for $\beta$ are $\beta = 1 - \alpha$ (Pareschi Russo) and $\beta = 1$. Qin and Zhang's method is a Pareschi Russo method with $\alpha = 1/4$. In both cases, the method is A-stable if $\alpha \geq 1/4$ and L-stable if $\alpha = 1 \pm \sqrt{2} / 2$.

The third-order conditions impose
$$\begin{array}{c|cc}
\frac{1}{2} - \frac{\sqrt{3}}{6} x & \frac{1}{2} - y x & (y - \frac{\sqrt{3}}{6}) x \\
\frac{1}{2} + \frac{\sqrt{3}}{6} x^{-1} & (y + \frac{\sqrt{3}}{6}) x^{-1} & \frac{1}{2} - y x^{-1} \\ \hline
& \frac{1}{1 + x^{2}} & \frac{x^{2}}{1 + x^{2}}
\end{array}$$
for some $x \neq 0$ and $y \in \RR$. Choosing $y = \sqrt{3} / 6$ yields a diagonally-implicit scheme, and even a singly-diagonally-implicit one with $x = \pm 1$. The choice ($x = -1$, $y = \sqrt{3} / 6$) is known as the Crouzeix method.

Choosing $x = 1$ and $y = 1/4$ produces a Gauss-Legendre scheme.

\backtonotes