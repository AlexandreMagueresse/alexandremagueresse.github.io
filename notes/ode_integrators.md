+++
title = "Ordinary Differential Equations"
hasmath = true
hascode = false
date = Date(2025, 03, 31)

rss_title = "Ordinary Differential Equations"
rss_description = "Ordinary Differential Equations"
rss_pubdate = Date(2025, 03, 31)

tags = ["research"]
+++

\backtonotes

# Ordinary Differential Equations

\tableofcontents

## General framework

Let $\mb{f} \in C(\RR \times \RR^{d}, \RR^{d})$ be continuous in the first variable and Lipschitz continuous in the second variable. For all $\mb{p} \in \RR^{d}$, the Picard--Lindelöf theorem ensures the existence of an open interval $I \subset \RR$ containing $0$ and a unique $\mb{u}: I \to \RR^{d}$ such that
$$\forall t \in I, \quad \dot{\mb{u}}(t) = \mb{f}(t, \mb{u}(t)), \qquad \mb{u}(0) = \mb{p}.$$
Besides, $\mb{u}$ depends continuously on $\mb{u}$; in other words, this initial value problem is well-posed.

We are willing to approximate the flow of $\mb{f}$ in the interval $[0, T]$ for some $T \in I \cap \RR_{+}$. For simplicity, we construct an approximate flow using constant time steps. Let $n \geq 1$, define $h = T / n$ and $t_{k} = k h$ for $k \in \{0, \ldots, n\}$. We consider a general marching procedure described by the following framework:
* A **starting map** $\ms{S}_{h}: \RR^{d} \to \md{S}$ embeds the initial condition into a state space $\md{S}$,
* A **marching map** $\ms{M}_{h}: \md{S} \to \md{S}$ evolves the state for one time step,
* A **finishing map** $\ms{F}_{h}: \md{S} \to \RR^{d}$ converts the state space into the solution space.
We define the recurrences $(\mb{s}_{k})_{0 \leq k \leq n}$ and $(\mb{u}_{k})_{0 \leq k \leq n}$ by
$$\mb{s}_{0} = \ms{S}_{h}(\mb{p}), \qquad \mb{s}_{k+1} = \ms{M}_{h}(\mb{s}_{k}), \qquad \mb{u}_{k} = \ms{F}_{h}(\mb{s}_{k}).$$
In other words, $\mb{s}_{k} = \ms{M}_{h}^{k} \circ \ms{S}_{h}(\mb{u}_{0})$ and $\mb{u}_{k} = \ms{F}_{h} \circ \ms{M}_{h}^{k} \circ \ms{S}_{h}(\mb{u}_{0})$. We want to design the scheme $(\ms{S}_{h}, \ms{M}_{h}, \ms{F}_{h})$ so that $\mb{u}_{k}$ approximates $\mb{u}(t_{k})$.

Let $\ms{E}_{h}: \RR^{d} \to \RR^{d}$ denote the exact flow of $\mb{f}$ for a time step $h$, that is $\ms{E}(\mb{u}(t)) = \mb{u}(t + h)$. A first idea is to compare the approximate and continuous solutions at time $T$. The corresponding error is called the **global truncation error** and is defined as
$$\ms{GTE}(h) \doteq \norm{\ms{F}_{h} \circ \ms{M}_{h}^{n} \circ \ms{S}_{h}(\mb{p}) - \ms{E}_{h}^{n}(\mb{p})}.$$
We are only in the dependence of $\ms{GTE}$ on $h$ and the derivatives of $\mb{f}$; not on $\mb{p}$. It is easier to look at the error after a single step. This is called the **local truncation error**,
$$\ms{LTE}(h) \doteq \norm{\ms{F}_{h} \circ \ms{M}_{h} \circ \ms{S}_{h}(\mb{p}) - \ms{E}_{h}(\mb{p})}.$$

We can now state the consistency and convergence of a scheme.

\definition{Consistency}{
A scheme is **consistent with order** $p$ if $\ms{LTE}(h) = O(h^{p})$. When $p = 0$, this property is called **pre-consistency**. When $p = 1$, this property is called **consistency**.
}

\definition{Convergence}{
A scheme is **convergent with order** $p$ if $\ms{GTE}(h) = O(h^{p+1})$.
}

We now move to the linear stability of a scheme. It is defined in terms of the behaviour of the scheme when applied to the test problem $\mb{f}(t, \mb{u}) = \lambda \mb{u}$ for $\lambda \in \CC$. The exact solution is $\mb{u}(t) = \exp(\lambda t) \mb{p}$; in particular $\mb{u}$ vanishes at infinity when $\Re \lambda < 0$. We are interested in schemes that mimic this property numerically.

\definition{Linear stability}{
The **stability function** of a scheme is the transfer function $\mb{M}: \CC \to \RR^{d \times d}$ involved in $\mb{u}_{k+1} = \mb{M}(\lambda h) \mb{u}_{k}$ when applied to $\mb{f}(t, \mb{u}) = \lambda \mb{u}$.
* Zero-stability / $D$-stability: $\mb{M}(0)$ is bounded, that is, $\norm{\mb{M}(0)^{k}}$ is bounded.
* Strict zero-stability: $\mb{M}(0)$ is is convergent, that is, $\norm{\mb{M}(0)^{k}} \to 0$.

The scheme is said to be absolute stable at $z = \lambda h \in \CC$: $\rho(\mb{M}(z)) < 1$. The **region of absolute stability** of the scheme is defined as
$$\mc{R} \doteq \{z \in \CC, \rho(\mb{M}(z)) < 1\}.$$
The **interval of stability** is $\mc{R} \cap \RR$. Related stability notions are as follows:
* $A$-stability: $\{z \in \CC, \Re z < 0\} \subset \mc{R}$.
* $A(\alpha)$-stability: $\{z \in \CC, \Re z \leq 0, \abs{\frac{\Im z}{\Re z}} \leq \tan \alpha\} \subset \mc{R}$.
* $A(0)$-stability: $A(\alpha)$-stability for some $\alpha > 0$.
* $A_{0}$-stability: $A(\alpha)$-stability for $\alpha = 0$.
* Stiff stability: $\{z \in \CC, \Re z < -C\} \cup \{z \in \CC, -C \leq \Re z < 0, \abs{\Im z} \leq D \} \subset \mc{R}$ for some $C, D > 0$.
* $I$-stability: $\{z \in \CC, \Re z = 0\} \subset \mc{R}$.
* $L$-stability / Super stability / Strong $A$ stability: $A$-stability and $\rho(\mb{M}(z)) \to 0$ when $z \to \infty$.
* $AN$-stability: equivalent of $A$-stability when $\mb{\lambda} \in \CC^{d}$.
}

We now move to some nonlinear stability properties. We are interested in dissipative problems where
$$\Re \inner{\mb{f}(t, \mb{u}) - \mb{f}(t, \mb{v})}{\mb{u} - \mb{v}} \leq 0.$$
In that case, if $\mb{u}_{0}, \mb{v}_{0} \in \RR^{d}$ are two initial conditions, then the corresponding solutions $\mb{u}, \mb{v}$ satisfy
$$\partial_{t} (\norm{\mb{u}(t) - \mb{v}(t)}^{2}) \leq 0,$$
so $\mb{u}$ and $\mb{v}$ merge at infinity. It is desirable to reproduce this behaviour numerically.

\definition{$B$-stability and $BN$-stability, $G$-stability}{
A scheme is **B-stable** if $\norm{\mb{u}_{n+1} - \mb{v}_{n+1}} \leq \norm{\mb{u}_{n} - \mb{v}_{n}}$ when applied to a monotonic autonomous problem and two arbitrary initial conditions. A scheme is **BN-stable** if the same condition holds for a non-autonomus problem. **G-stability** refers to the same property but in a norm induced by an SPD matrix.
}

\definition{RK-stability}{
A scheme is **RK-stable** if $\mb{M}(z)$ has a single non-zero eigenvalue. This eigenvalue is then interpreted as the stability function of a Runge-Kutta method.
}

\definition{Symplecticity}{
A scheme is **symplectic** if its stability function is a symplectic map when applied to a Hamiltonian system.
}

Similar stability and order notions can be defined in the state space or in some internal process of the marching procedure.

In the following, we briefly introduce the $\theta$-method, Runge-Kutta schemes and linear multi-step. We then provide a detailed analysis of general linear methods, which are a generalisation of theses schemes.

## $\theta$-method
The $\theta$-method is a simple family of schemes that includes the explicit and implicit Euler schemes, as well as the trapezoidal rule as special cases. We simply consider $\md{S} = \RR^{d}$, $\ms{S} = \ms{F} = \Id_{\RR^{d}}$ and $\ms{M}(\mb{s}_{k}) = \mb{s}_{k+1}$ is defined implicitly through
$$\mb{s}_{k+1} = \mb{s}_{k} + h \mb{f}((1 - \theta) t_{k} + \theta t_{k+1}, (1 - \theta) \mb{s}_{k} + \theta \mb{s}_{k+1}),$$
where $\theta \in \RR$ characterises the scheme. The choice $\theta = 0$ is the only explicit member of the family and is known as explicit Euler. The choice $\theta = 1$ corresponds to implicit Euler, and $\theta = 1/2$ is the trapezoidal rule.

The third-order Taylor expansion of the exact and approximate solutions are
$$\begin{align*}
\mb{u}(t_{k+1}) &= \mb{u}(t_{k}) + h \mb{f}(t_{k}, \mb{u}(t_{k})) + \frac{1}{2} h^{2} [\partial_{1} \mb{f}(t_{k}, \mb{u}(t_{k})) + \partial_{2} \mb{f}(t_{k}, \mb{u}(t_{k})) \mb{f}(t_{k}, \mb{u}(t_{k}))] + O(h^{3}), \\
\mb{u}_{k+1} &= \mb{u}_{k} + h \mb{f}(t_{k}, \mb{u}_{k}) + \theta h^{2} [\partial_{1} \mb{f}(t_{k}, \mb{u}_{k}) + \partial_{2} \mb{f}(t_{k}, \mb{u}_{k}) \mb{f}(t_{k}, \mb{u}_{k})] + O(h^{3}).
\end{align*}$$
Observe that regardless of $\theta$, the expansions $\mb{u}(t_{k+1})$ and $\mb{u}_{k+1}$ coincide up to $O(h)$, so the $\theta$-method is at least of order $1$. They coincide up to $O(h^{2})$ if and only if $\theta = 1/2$.

In the case of a linear first-order ODE, the definition of $\mb{u}_{k+1}$ is
$$\mb{u}_{k+1} = \mb{u}_{k} + (1 - \theta) z \mb{u}_{k} + \theta z \mb{u}_{k+1},$$
so we infer
$$\mb{M}(z) = \frac{1 + (1 - \theta) z}{1 - \theta z}.$$
Observe that
$$\abs{\mb{M}(z)} \leq 1 \iff (1 - 2 \theta) \abs{z}^{2} + 2 \Re(z) \leq 0.$$
We distinguish three classes:
* If $\theta < 1/2$, the stability region is the circle of radius $1 / (1 - 2 \theta)$ centred at $(-1/(1 - 2 \theta), 0)$. This scheme is not $A$-stable.
* If $\theta = 1/2$, the stability region is the whole left complex plane. The scheme is $A$-stable.
* If $\theta > 1/2$, the stability region includes the whole complex plane except the circle of radius $1 / (2 \theta - 1)$ and centred at $(1 /(2 \theta - 1), 0)$. In particular, this scheme is $A$-stable.
The scheme is only $L$-stable when $\theta = 1$.

## Runge-Kutta

The Runge-Kutta method is a multi-stage method consisting in enforcing a zero residual at intermediate times between $t_{k}$ and $t_{k+1}$, and forming $u_{k+1}$ from linear combinations of these intermediate solutions. Here again, $\md{S} = \RR^{d}$ and $\ms{S} = \ms{F} = \Id_{\RR^{d}}$. A RK scheme depends on $s \geq 1$, a matrix $\mb{A} \in \RR^{s \times s}$ and vectors $\mb{b}, \mb{c} \in \RR^{s}$. They are conveniently arranged in a Butcher tableau
$$\begin{array}{c|c}
\mb{c} & \mb{A} \\
\hline
& \mb{b}^{\ast}.
\end{array}$$
The marching procedure is defined as
$$\ms{M}(\mb{s}_{k}) = \mb{s}_{k} + h \sum_{i = 1}^{s} \mb{b}_{i} \mb{f}(\mb{w}_{i}),$$
where $\mb{w}_{1}, \ldots, \mb{w}_{s} \in \RR^{d}$ are such that
$$\mb{w}_{i} = \mb{s}_{k} + h \sum_{j = 1}^{s} \mb{A}_{ij} \mb{f}(t_{k} + \mb{c}_{i} h, \mb{w}_{j}).$$

### Linear stability
Applied to a linear ODE with constant step size $h$, letting $\mb{w} = (\mb{w}_{1}, \ldots, \mb{w}_{s}) \in \RR^{s}$, this recursion becomes
$$\mb{w} = \lambda (\mb{1}_{s} \mb{s}_{k} + h \mb{A} \mb{w}), \qquad \mb{u}_{k+1} = \mb{u}_{k} + h \mb{b}^{\ast} \mb{w}.$$
We infer $\mb{w} = \lambda (\mb{I} - z \mb{A})^{-1} \mb{1}_{s} \mb{u}_{k}$ and $\mb{u}_{k+1} = (1 + z \mb{b}^{\ast} (\mb{I} - z \mb{A})^{-1} \mb{1}) \mb{u}_{k}$, that is
$$\mb{M}(z) = 1 + z \mb{b}^{\ast} (\mb{I} - z \mb{A})^{-1} \mb{1}.$$

### Zero-stability, pre-consistency and consistency
All RK schemes are zero-stable and pre-consistent. The consistency condition is $\mb{b}^{\ast} \mb{1} = 1$. One usually assumes stage consistency, that is $\mb{A} \mb{1} = \mb{c}$.

### Order conditions
Higher order conditions can be studied using B-series: introduce $\mb{\xi} \in \ms{B}^{s}$ for each stage ($\mb{\xi} \sim \mb{u}(t + \mb{c} h)$). The order conditions read
$$\mb{\xi} = \mb{1} + \mb{A} \mb{\xi} \ms{D} = \ms{E}_{\mb{c}} + \ms{O}_{q+1}, \qquad \ms{E} = 1 + \mb{b}^{\ast} \mb{\xi} \ms{D} + \ms{O}_{p+1},$$
where $q$ is the stage-order and $p$ is the order.

## Linear multi-step

Linear multi-step methods store previous iterates and predict the next. As notable examples, this class of methods includes Adams-Moulton, Adams-Bashford and Backward Differentiation Formula (BDF) methods. 

In this setting, $\md{S} = (\RR^{d})^{r}$ for some $r \geq 1$, $\ms{S}$ can be a Runge-Kutta method and represents $\mb{u}(k h)$ for $k \in \{0, \ldots, r - 1\}$. In that case $\ms{F}$ simply extracts the first component of the state, that is $\ms{F}(\mb{s}_{1}, \ldots, \mb{s}_{r}) = \mb{s}_{1}$. The marching procedure is defined as
$$\ms{M}(\mb{s}_{1}, \ldots, \mb{s}_{r}) = (\mb{s}_{0}, \mb{s}_{1}, \ldots, \mb{s}_{r-1}),$$
where $\mb{s}_{0} \in \RR^{d}$ solves
$$\mb{s}_{0} = \sum_{i = 1}^{r} \mb{\alpha}_{i} \mb{s}_{i} + h \sum_{i = 0}^{r} \mb{\beta}_{i} \mb{f}(t_{k} - (i - 1) h, \mb{s}_{i}).$$
Here $\mb{\alpha} \in \RR^{r}$ and $\mb{\beta} \in \RR^{r+1}$ are the parameters of the method.

### Linear stability
The stability matrix is the companion matrix of the polynomial $\pi(w, z) = \rho(w) - z \sigma(w)$, so the stability condition at a given $z \in \CC$ is that the roots of $\pi(w, z)$ are in the unit circle.

### Zero-stability, pre-consistency and consistency
It is common to introduce the polynomials
$$\rho(z) = z^{r} - \sum_{i = 1}^{r} \mb{\alpha}_{i} z^{r - i}, \qquad \sigma(z) = \sum_{i = 0}^{r} \mb{\beta}_{i} z^{r - i}.$$
The zero-stability requires the roots of $\rho$ to lie in the unit circle. The pre-consistency condition is then $\sum_{i = 1}^{r} \mb{\alpha}_{i} = 1$, that is $\rho(1) = 0$. The consistency condition is $\sum_{i = 0}^{r} \mb{\beta}_{i} = r - \sum_{i = 1}^{r} \mb{\alpha}_{i} (r - i) $, that is $\rho'(1) - \sigma(1) = 0$.

### Order conditions
The order conditions are $\pi(\exp(z), z) = \rho(\exp(z)) - z \sigma(\exp(z)) = O(z^{p+1})$. Alternatively, using the formalism of B-series, the order conditions are written
$$\ms{E}^{r} = \sum_{i = 1}^{r} \mb{\alpha}_{i} \ms{E}^{r - i} + \sum_{i = 0}^{r} \mb{\beta}_{i} \ms{E}^{r - i} \ms{D} + \ms{O}_{p+1}.$$

## General linear methods

Runge-Kutta and linear multi-step methods can be examined under the broad class of general linear methods (GLM). In this class of methods, we allow for $r \geq 1$ reused steps and $s \geq 1$ internal stages. Runge-Kutta methods are recovered for $r = 1$, while linear multi-step methods correspond to $s = 1$. GLM were introduced to offer more flexibility than RK and LM methods, provide a better understanding of order conditions, and break order barriers.

The state space is thus $\md{S} = (\RR^{d})^{r}$. The starting and finishing procedures depend on the particular scheme; we describe them below. The marching procedure has the form
$$\ms{M}_{h}(\mb{s})_{i} = \mb{V}_{ij} \mb{s}_{j} + h \mb{B}_{ij} \mb{f}(\mb{w}_{j}),$$
where $\mb{w}_{1}, \ldots, \mb{w}_{s} \in \RR^{d}$ are defined implicitly via
$$\mb{w}_{i} = \mb{U}_{ij} \mb{s}_{j} + h \mb{A}_{ij} \mb{f}(\mb{W}_{j}).$$

These schemes are characterised by the matrices $\mb{A} \in \RR^{s \times s}$, $\mb{B} \in \RR^{r \times s}$, $\mb{U} \in \RR^{s \times r}$ and $\mb{V} \in \RR^{r \times r}$, as well as assumptions on the interpretation of the state variables, the shape of the stage variables and the finishing procedure. One usually assume that the starting procedure is such that the state at time $t$ represents approximations of $\mb{u}(t)$ involving higher-order derivatives, that is
$$\mb{s}_{i}(t) = \sum_{k = 0}^{p} \mb{\alpha}_{0, k} \mb{u}(t) + O(h^{p+1}).$$
where $\mb{\alpha}_{0}, \ldots, \mb{\alpha}_{p} \in \RR^{r}$. We do not focus on the design of the starting procedure for now. The internal stages are assumed to represent
$$\mb{w}_{i}(t) = \mb{u}(t + \mb{c}_{i} h) + O(h^{2})$$
for some $\mb{c} \in \RR^{s}$. Finally, we assume that the finishing procedure is just a linear combination of the state vectors, that is
$$\ms{F}(\mb{s}_{1}, \ldots, \mb{s}_{r}) = \sum_{i = 1}^{r} \mb{\beta}_{i} \mb{s}_{i},$$
for some $\mb{\beta} \in \RR^{r}$.

### Linear stability
Applied to the linear ODE $\mb{f}(t, \mb{u}) = \lambda \mb{u}$, the recursions defining $\mb{w}$ and $\mb{s}_{k}$ read
$$\mb{w} = \mb{U} \mb{s}_{k} + z \mb{A} \mb{w}, \qquad \mb{s}_{k+1} = \mb{V} \mb{s}_{k} + z \mb{B} \mb{w}.$$
We readily infer $\mb{s}_{k+1} = (\mb{V} + z \mb{B} (\mb{I} - z \mb{A})^{-1} \mb{U}) \mb{s}_{k}$, and thus
$$\mb{u}_{k} = \ms{F}_{h} \circ (\mb{V} + z \mb{B} (\mb{I} - z \mb{A})^{-1} \mb{U})^{k} \circ \ms{S}_{h}(\mb{p}).$$
Strictly speaking, the linear stability analysis requires the knowledge of $\ms{S}_{h}$ and $\ms{F}_{h}$, but one usually directly relates it to the stability in the state space, and introduces
$$\mb{M}(z) = \mb{V} + z \mb{B} (\mb{I} - z \mb{A})^{-1} \mb{U}.$$

### Zero-stability, pre-consistency and consistency
Applying a GLM to $\mb{f} = \mb{0}$, we obtain
$$\mb{u}_{k} = \ms{F}_{h} \circ \mb{V}^{k} \circ \ms{S}_{h}(\mb{p}).$$
In particular for $k = 0$, one must have $\ms{F}_{h} \circ \ms{S}_{h} = \Id_{\RR^{d}}$, so $\ms{S}_{h}$ must be left-invertible and $\ms{F}_{h}$ has to be a left-inverse of $\ms{S}_{h}$. Besides, $\mb{V}$ must be power-bounded for $\mb{u}_{k}$ to remain bounded.

The pre-consistency and consistency conditions are $\mb{\beta}^{\ast} \mb{V} \mb{\alpha}_{0} = 1$ and $\mb{\beta}^{\ast} (\mb{B} \mb{1} + \mb{V} \mb{\alpha}_{1}) = 1$. In fact, these are projections on the output space of the pre-consistency and consistency conditions in the state space, $\mb{V} \mb{\alpha}_{0} = \mb{\alpha}_{0}$ and $\mb{\alpha}_{0} + \mb{\alpha}_{1} = \mb{B} \mb{1} + \mb{V} \mb{\alpha}_{1}$, respectively. It is often of interest to look for the pre-consistency and consistency at the stage level. These conditions are $\mb{U} \mb{\alpha}_{0} = \mb{1}$ and $\mb{c} = \mb{A} \mb{1} + \mb{U} \mb{\alpha}_{1}$, respectively.

### Order conditions
The analysis of GLM is simplified through the formalism of B-series. We introduce $\mb{\xi} \in \ms{B}^{s}$ to represent the stage vectors (corresponding to $\mb{u}(t + \mb{c} h)$) and $\mb{\eta} \in \ms{B}^{r}$ for the state vectors (corresponding to $\mb{\alpha}_{k} \mb{u}^{(k)}(t)$). They are related by
$$\mb{\xi} = \mb{U} \mb{\eta} + \mb{A} \mb{\xi} \ms{D} = \ms{E}_{\mb{c}} + \ms{O}_{q+1}, \qquad \ms{E} \mb{\eta} = \mb{V} \mb{\eta} + \mb{B} \mb{\xi} \ms{D} + \ms{O}_{p+1}, \qquad \ms{E} = \mb{\beta}^{\ast} \ms{E} \mb{\eta} + \ms{O}_{o+1}.$$
Here $q$ is the stage order, $p$ is the state order and $o$ is the order of the method.

\backtonotes