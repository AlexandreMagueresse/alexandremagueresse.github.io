+++
title = "Notions of continuity"
hasmath = true
hascode = false
date = Date(2025, 05, 9)

rss_title = "Notions of continuity"
rss_description = "Notions of continuity"
rss_pubdate = Date(2025, 05, 9)

tags = ["research"]
+++

\backtonotes

# Notions of continuity

Let $(X, d_{X})$, $(Y, d_{Y})$ and $(Z, d_{Z})$ be metric spaces. For all $c \in X$ and $r > 0$, let $B_{X}(c, r)$ denote the closed ball of center $c$ and radius $r$; that is,
$$B_{X}(c, r) \doteq \{x \in X, d_{X}(c, x) \leq r\}.$$
We use the same notation in $Y$ and $Z$. We always equip $\RR$ with its usual metric $d_{\RR}(x, y) \doteq \abs{y - x}$.

\tableofcontents

## Boundedness

The set of maps from $X$ to $Y$ is denoted $\mc{F}(X, Y)$.

\definition{Boundedness}{
We say that $f \in \mc{F}(X, Y)$ is **bounded** if $f(X)$ is bounded as a subset of $Y$; that is,
$$\diam(f, X, Y) \doteq \sup \{d_{Y}(f(x), f(y)), x \in X, y \in X\} < \infty.$$
}
The subset of $\mc{F}(X, Y)$ consisting in bounded maps is denoted $\mc{B}(X, Y)$.

\proposition{
The map $d_{\mc{B}(X, Y)}: \mc{B}(X, Y) \times \mc{B}(X, Y) \to \RR$ defined by
$$d_{\mc{B}(X, Y)}(f, g) \doteq \sup \{d_{Y}(f(x), g(x)), x \in X\}$$
is a metric that turns $\mc{B}(X, Y)$ into a metric space.
}
\proof{
By construction, $d_{\mc{B}(X, Y)}$ inherits the non-negativity and symmetry from $d_{Y}$. Suppose $f, g \in \mc{B}(X, Y)$ are such that $d_{\mc{B}(X, Y)}(f, g) = 0$. Then $d_{Y}(f(x), g(x)) = 0$, for all $x \in X$, which is equivalent to $f(x) = g(x)$ for all $x \in X$; that is, $f = g$. Finally, given $f, g, h \in \mc{B}(X, Y)$ and $x \in X$, the triangle inequality for $d_{Y}$ implies
$$d_{Y}(f(x), h(x)) \leq d_{Y}(f(x), g(x)) + d_{Y}(g(x), h(x)).$$
Taking the supremum on $x \in X$ and using the properties of the supremum, we reach $d_{\mc{B}(X, Y)}(f, h) \leq d_{\mc{B}(X, Y)}(f, g) + d_{\mc{B}(X, Y)}(g, h)$. This shows $d_{\mc{B}(X, Y)}$ is a metric on $\mc{B}(X, Y)$.
}

Note that if $f, g \in \mc{B}(X, Y)$, then
$$\begin{align*}
d_{Y}(f(x), g(x)) & \leq d_{Y}(f(x), f(y)) + d_{Y}(f(y), g(z)) + d_{Y}(g(z), g(x)) \\
& \leq \diam(f, X, Y) + d_{Y}(f(y), g(z)) + \diam(g, X, Y)
\end{align*}$$
for all $x, y, z \in X$. Taking the supremum on $x$ and the infimum on $y, z$, we find
$$d_{\mc{B}(X, Y)}(f, g) \leq \diam(f, X, Y) + \diam(g, X, Y) + \inf \{d_{Y}(f(y), g(z)), y \in X, z \in X\}.$$
In particular, if $f(X) \cap g(X) \neq \varnothing$, the infimum above is $0$.

## Continuity

\definition{Local continuity}{
A map $f: X \to Y$ is **(locally) continuous** at $x \in X$ if for all $\eps > 0$, there exists $\delta > 0$ such that $f$ sends $B_{X}(x, \delta)$ into $B_{Y}(f(x), \eps)$. More precisely, $d_{Y}(f(x), f(y)) \leq \eps$ for all $y \in Y$ such that $d_{X}(x, y) \leq \delta$.
}

\proposition{
* If $f \in \mc{F}(X, Y)$ is continuous at $x \in X$ and $g \in \mc{F}(Y, Z)$ is continuous at $f(x)$, then $g \circ f \in \mc{F}(X, Z)$ is continuous at $x$.
* If $Y$ is a $\md{K}$-vector space and $f, g \in \mc{F}(X, Y)$ are continuous at $x \in X$, then $\alpha f + \beta g \in \mc{F}(X, Y)$ are continuous at $x$ for all $\alpha, \beta \in \md{K}$.
* If $Y$ is an algebra and $f, g \in \mc{B}(X, Y)$ are continuous at $x \in X$, then $f g \in \mc{B}(X, Y)$ is continuous at $x$.
}
\proof{
Let $f \in \mc{F}(X, Y)$ be continuous at $x \in X$ and $g \in \mc{F}(Y, Z)$ be continuous at $f(x)$. Let $\eps > 0$. Since $g$ is continuous at $f(x)$, there exists $\delta_{g} > 0$ such that $g(B_{Y}(f(x), \delta_{g})) \subset B_{Z}((g \circ f)(x), \eps)$. Since $f$ is continuous at $x$, there exists $\delta_{f} > 0$ such that $f(B_{X}(x, \delta_{f})) \subset B_{Y}(f(x), \delta_{g})$. Then choosing $\delta = \delta_{f}$, we have $(g \circ f)(B_{X}(x, \delta)) \subset B_{Z}((g \circ f)(x), \eps)$ so $g \circ f$ is continuous at $x$.

Suppose now that $Y$ is a vector space. Let $f, g \in \mc{F}(X, Y)$ be continuous at $x \in X$. Let $\alpha, \beta \in \md{K}$. For convenience, denote $h = \alpha f + \beta g$. Let $\eps > 0$ and define $\eps' = \eps / (\abs{\alpha} + \abs{\beta} + 1)$. Since $f$ and $g$ are continuous at $x$, there exist $\delta_{f}, \delta_{g} > 0$ such that $f(B_{X}(x, \delta_{f})) \subset B_{Y}(f(x), \eps')$ and similarly for $g$. Choosing $\delta = \min(\delta_{f}, \delta_{g}) > 0$, we then have, for all $y \in B_{X}(x, \delta)$,
$$d_{Y}(h(x), h(y)) \leq \abs{\alpha} d_{Y}(f(x), f(y)) + \abs{\beta} d_{Y}(g(x), g(y)) \leq (\abs{\alpha} + \abs{\beta}) \eps' \leq \eps,$$
so $h$ is continuous at $x$.

Finally, suppose $Y$ is an algebra and $f, g \in \mc{B}(X, Y)$ are continuous at $x$. Let $\epsilon > 0$ and define $\epsilon' = \epsilon / (\norm{f}_{\infty} + \norm{g}_{\infty} + 1)$. Since $f$ and $g$ are continuous at $x$, there exist $\delta_{f}, \delta_{g} > 0$ such that $f(B_{X}(x, \delta_{f})) \subset B_{Y}(f(x), \eps')$ and similarly for $g$. Choosing $\delta = \min(\delta_{f}, \delta_{g}) > 0$, we have, for all $y \in B_{X}(x, \delta)$, the triangle inequality yields
$$\begin{align*}
d_{Y}((f g)(x), (f g)(y)) & = d_{Y}(f(x) g(x), f(x) g(y)) + d_{Y}(f(x) g(y), f(y) g(y)) \\
& = \abs{f(x)} d_{Y}(g(x), g(y)) + \abs{g(y)} d_{Y}(f(x), f(y)) \\
& \leq (\norm{f}_{\infty} + \norm{g}_{\infty}) \epsilon' \\
& \leq \epsilon,
\end{align*}$$
so $f g$ is continuous at $x$.
}

There is more to say about maps that are continuous everywhere.

\definition{Global continuity}{
If $f: X \to Y$ is continuous everywhere in $X$, then $f$ is said to be **(globally) continuous**.
}

The set of continuous maps from $X$ to $Y$ is denoted $\mc{C}(X, Y)$.

We now give a few examples to illustrate the difference between locally and globally continuous functions.

\example{
The **identity map** $\Id_{X}: X \to X$ belongs to $\mc{C}(X, X)$. Let $\eps > 0$ and $x \in X$. Let $\delta = \eps$ and $y \in B_{X}(x, \delta)$. Then $d_{X}(\Id_{X}(x), \Id_{X}(y)) = d_{X}(x, y) \leq \delta = \eps$.
}

\example{
Let $z \in Y$. The **constant map** $\tilde{z}: X \to Y$ defined by $\tilde{z}(x) = z$ belongs to $\mc{C}(X, Y)$. Let $\eps > 0$ and $x \in X$. Let $\delta > 0$ and $y \in B_{X}(x, \delta)$. Then $d_{X}(\tilde{z}(x), \tilde{z}(y)) = d_{X}(z, z) = 0 \leq \eps$.
}

\example{
Let $z \in X$. The **distance map** $d_{z}: X \to \RR$ defined by $d_{z}(x) = d_{X}(x, z)$ belongs to $\mc{C}(X, \RR)$. Let $\eps > 0$ and $x \in X$. Let $\delta = \eps$ and $y \in B_{X}(x, \delta)$. Then the reverse triangle inequality for metric spaces provides $\abs{d_{z}(y) - d_{z}(x)} = \abs{d_{X}(y, z) - d_{X}(x, z)} \leq d_{X}(x, y) \leq \delta = \eps$.
}

\example{
Let $\alpha \geq 0$. The **power function** $p_{\alpha}: \RR_{+} \to \RR$ defined by $p_{\alpha}(x) = x^{\alpha}$ belongs to $\mc{C}(\RR_{+}, \RR)$. Let $\eps > 0$ and $x \in \RR_{+}$. We separate two cases depending on the position of $\alpha$ relative to $1$.
* If $\alpha \in [0, 1]$, define $\delta = \eps^{1/\alpha}$. The case $y = x$ being trivial, we assume $y \neq x$ and write
$$\abs{y^{\alpha} - x^{\alpha}} = \underbrace{\frac{\abs{y^{\alpha} - x^{\alpha}}}{\abs{y - x}^{\alpha}}}_{\phi(x, y)} \abs{y - x}^{\alpha} \leq \delta^{\alpha} = \eps.$$
Indeed, the function $\phi$ is homogeneous in $x$ and $y$ and since $x \neq y$, we introduce $t = \min(x, y) / \max(x, y) \in [0, 1)$ and rewrite
$$\phi(x, y) = \psi(t), \qquad \psi: [0, 1) \ni t \mapsto \frac{1 - t^{\alpha}}{(1 - t)^{\alpha}}.$$
A quick study of the function $\psi$ shows that it is bounded by $1$.
* If $\alpha > 1$, define $\delta > 0$ such that $\alpha (x + \delta)^{\alpha - 1} \delta = \eps$ (such a $\delta$ exists because $t \mapsto (x + t)^{\alpha - 1} t$ is increasing). The mean value theorem ensures the existence of $c \in (x, y)$ such that
$$\abs{y^{\alpha} - x^{\alpha}} = \alpha \abs{\int_{x}^{y} t^{\alpha - 1} dt} = \alpha c^{\alpha - 1} \abs{y - x} \leq \alpha \max(x, y)^{\alpha - 1} \abs{y - x} \leq \alpha (x + \delta)^{\alpha - 1} \delta = \eps.$$
}

\example{
Define the **sign function** $s_{a}: \RR \to \RR$ defined by $s_{a}(x) = -1$ if $x < 0$, $s_{a}(x) = +1$ if $x > 0$ and $s_{a}(0) = a$ for some $a \in \RR$. We will show that $s_{a}$ cannot be made continuous at $0$. Let $x = 0$ and $y \in \RR$. If $y > 0$, then $s_{a}(y) - s_{a}(x) = 1 - a$, which is independent of $y$. The only way to make this smaller than $\eps$ for all $\eps > 0$ is to choose $a = 1$. Conversely, if $y < 0$, then $s_{a}(y) - s_{a}(x) = - 1 - a$ and the only way to make this smaller than $\eps$ for all $\eps > 0$ is to choose $a = -1$. There is no choice of $a$ that makes $s_{a}$ continuous.
}

The last example would motivate a notion of "directional continuity", which is a generalisation of one-sided continuity to metric spaces.

\propositionT{Structure of $\mc{C}(X, Y)$}{
* If $f \in \mc{C}(X, Y)$ and $g \in \mc{C}(Y, Z)$, then $g \circ f \in \mc{C}(X, Z)$.
* If $Y$ is a vector space, then $\mc{C}(X, Y)$ is a subvector space of $\mc{F}(X, Y)$.
* If $f, g \in \mc{C}(X, Y) \cap \mc{B}(X, Y)$, then $f g \in \mc{C}(X, Y)  \cap \mc{B}(X, Y)$.
}
\proof{
The previous proposition on the stability of local continuity under composition, linear combinations and product readily extends to global continuity. We have proved that the constant function $\tilde{0_{Y}}: X \to Y$ is continuous in the second example. This shows that $\mc{C}(X, Y)$ is a vector space when $Y$ is one.
}

## Uniform continuity

In the definition of continuity, $\delta$ is allowed to depend on $x$ and $\eps$. The following stronger definition of continuity requires that $\delta$ be independent of $x$.

\definition{Uniform continuity}{
A map $f: X \to Y$ is **uniformly continuous** if for all $\eps > 0$, there exists $\delta > 0$ such that $f$ sends any ball of radius $\delta$ in $X$ into a ball of radius $\eps$ in $Y$. More precisely, $d_{Y}(f(x), f(y)) \leq \eps$ for all $x, y \in X$ such that $d_{X}(x, y) \leq \delta$.
}

The set of uniformly continuous functions from $X$ to $Y$ is denoted $\mc{U}(X, Y)$.

\example{
From the previous examples, looking at the dependence of $\delta$ on $\eps$, we observe that the identity map, the constant map, the distance map and the power function with $\alpha \in [0, 1]$ are uniformly continuous. However, the power function with $\alpha > 1$ is not uniformly continuous.
}

\propositionT{Structure of $\mc{U}(X, Y)$}{
* If $Y$ is a vector space, then $\mc{U}(X, Y)$ is a subvector space of $\mc{C}(X, Y)$.
* If $f \in \mc{U}(X, Y)$ and $g \in \mc{U}(Y, Z)$, then $g \circ f \in \mc{U}(X, Z)$.
* If $Y$ is a normed algebra and $f, g \in \mc{U}(X, Y)$ are bounded, then $fg \in \mc{U}(X, Y)$.
}
\proof{
This proof is identical to its counterpart for $\mc{C}(X, Y)$. The only difference is that $\delta$ is defined before $x$.
}

## Modulus of continuity

It is useful to characterise the dependence of $\delta$ on $\eps$ for a uniformly continuous function. This is what the modulus of continuity measures. We first identify candidate moduli of continuity.

\definition{Modulus of continuity}{
A function $\omega: \RR_{+} \to \RR_{+}$ is a **modulus of continuity** if $\omega$ is non-decreasing, $\omega(0) = 0$ and $\omega$ is continuous at $0$.
}

The set of moduli of continuity is written $M$. Note that $M$ is stable under non-negative linear combinations and composition. We can now characterise uniform continuity with moduli of continuity.

\definition{Uniform continuity with modulus}{
A function $f: X \to Y$ is **uniformly continuous with modulus** $\omega \in M$ if $d_{Y}(f(x), f(y)) \leq \omega(d_{X}(x, y))$ for all $x, y \in X$. We also simply say that $f$ is $\omega$-uniformly continuous, $\omega$-UC for short, and we write $f \in \mc{U}(\omega, X, Y)$.
}

We first show that if $f \in \mc{U}(X, Y)$, then $f \in \mc{U}(\omega, X, Y)$ for some well-chosen $\omega \in M$.

\propositionT{Minimal modulus of continuity}{
If $f \in \mc{U}(X, Y)$ and define $\omega_{f} \in M$ as
$$\omega_{f}(\delta) = \sup \{d_{Y}(f(x), f(y)), x \in X, y \in X, d_{X}(x, y) \leq \delta\}.$$
Then $f \in \mc{U}(\omega_{f}, X, Y)$.
}
\proof{
Let us show that $\omega_{f} \in M$. When $\delta = 0$, one must have $x = y$ in the definition of $\omega_{f}(0)$, so $\omega_{f}(0) = 0$. Besides, $\omega_{f}$ is non-increasing by construction. Now given $\eps > 0$, the uniform continuity of $f$ ensures the existence of $\delta > 0$ such that $d_{Y}(f(x), f(y)) \leq \eps$ for all $x, y \in X$ with $d_{X}(x, y) \leq \delta$. Taking the supremum on that region, we find $\omega(t) \leq \eps$ for all $t \in [0, \delta]$. This is exactly the definition of the continuity of $\omega_{f}$ at $0$.

Finally, by construction, for all $\eps > 0$, choosing $\delta > 0$ such that $\omega(\delta) \leq \eps$ implies that $d_{Y}(f(x), f(y)) \leq \eps$ whenever $d_{X}(x, y) \leq \delta$. This shows $f \in \mc{U}(\omega_{f}, X, Y)$.
}

We now show that uniform continuity is equivalent to having a modulus of continuity.

\proposition{
$f \in \mc{U}(X, Y)$ if and only if there exists $\omega \in M$ such that $f \in \mc{U}(\omega, X, Y)$.
}
\proof{
Suppose $f \in \mc{U}(\omega, X, Y)$ for some $\omega \in M$. Let $\eps > 0$. Since $\omega$ is non-decreasing, there exists $\delta > 0$ such that $\omega(\delta) \leq \eps$ (if $\omega$ is bounded and $\eps$ is larger than the maximum of $\omega$, then any choice of $\delta$ is acceptable). For all $x, y \in X$ such that $d_{X}(x, y) \leq \delta$, we have $d_{Y}(f(x), f(y)) \leq \omega(d_{X}(x, y)) \leq \omega(\delta) \leq \eps$. This shows $f \in \mc{U}(X, Y)$.

Conversely, we have already seen that $f \in \mc{U}(X, Y)$ implies $f \in \mc{U}(\omega_{f}, X, Y)$.
}

Note that if a map admits a modulus of continuity, then it admits infinitely many. Indeed, if $\omega, \eta \in M$ are such that $\eta \geq \omega$ and $f \in \mc{U}(\omega, X, Y)$, then $f \in \mc{U}(\eta, X, Y)$. Still, a uniformly continuous function $f$ admits a minimal modulus of continuity.

\propositionT{Minimal modulus of continuity}{
Let $\omega \in M$ such that $f \in \mc{U}(\omega, X, Y)$. Then $\omega \geq \omega_{f}$.
}
\proof{
Let $\omega \in M$ such that $f \in \mc{U}(\omega, X, Y)$. Then given $\delta > 0$, we have $d_{Y}(f(x), f(y)) \leq \omega(\delta)$ for all $x, y \in X$ with $d_{X}(x, y) \leq \delta$. Taking the supremum on that region, we find $\omega_{f}(\delta) \leq \omega(\delta)$.
}

\propositionT{Structure of $\mc{U}(\omega, X, Y)$}{
* If $f \in \mc{U}(\omega_{f}, X, Y)$ and $g \in \mc{U}(\omega_{g}, Y, Z)$, then $g \circ f \in \mc{U}(\omega_{g} \circ \omega_{f}, X, Y)$.
* If $Y$ is a vector space and $f \in \mc{U}(\omega_{f}, X, Y)$ and $g \in \mc{U}(\omega_{g}, X, Y)$, then $\alpha f + \beta g \in \mc{U}(\abs{\alpha} \omega_{f} + \abs{\beta} \omega_{g}, X, Y)$.
* If $Y$ is a normed algebra and $f \in \mc{U}(\omega_{f}, X, Y)$ is bounded and $g \in \mc{U}(\omega_{g}, X, Y)$ is bounded, then $f g \in \mc{U}(\norm{f}_{\mc{C}(X, Y)} \omega_{g} + \norm{g}_{\mc{C}(X, Y)} \omega_{f})$.
}

## Application
We conclude with a short application to the error analysis of the approximation of a function $f \in \mc{U}(\omega, I \subset \RR, \RR)$ by its Bernstein coefficient, defined by
$$B_{n}(f)(x) = \sum_{k = 0}^{n} \binom{n}{k} x^{k} (1 - x)^{n - k} f\left(\frac{k}{n}\right),$$
for all $n \geq 1$. Let $x \in I$ and $\delta \leq 1/n$. We compute
$$\begin{align*}
\abs{f(x) - B_{n}(f)(x)} & \leq \sum_{k = 0}^{n} \binom{n}{k} x^{k} (1 - x)^{n - k} \abs{f(x) - f\left(\frac{k}{n}\right)} \\
& \leq \sum_{k = 0}^{n} \binom{n}{k} x^{k} (1 - x)^{n - k} \omega\left(f, \abs{x - \frac{k}{n}}\right) \\
& \leq \sum_{k = 0}^{n} \binom{n}{k} x^{k} (1 - x)^{n - k} \left(\floor{\delta^{-1} \abs{x - \frac{k}{n}}} + 1\right) \omega\left(f, \delta\right) \\
&= \left(1 + \sum_{k = 0}^{n} \binom{n}{k} x^{k} (1 - x)^{n - k} \floor{\delta^{-1} \abs{x - \frac{k}{n}}}\right) \omega\left(f, \delta\right) \\
&\leq \left(1 + \delta^{-2} \sum_{k = 0}^{n} \binom{n}{k} x^{k} (1 - x)^{n - k} \left(x - \frac{k}{n}\right)^{2}\right) \omega\left(f, \delta\right) \\
&= \left(1 + \delta^{-2} n^{-1} x(1 - x)\right) \omega\left(f, \delta\right).
\end{align*}$$
In the last inequality, we used the fact that if $k \in \{0, \ldots, n\}$ is such that $\abs{x - \frac{k}{n}} < \delta$, then $\floor{\delta^{-1} \abs{x - \frac{k}{n}}} = 0$ and otherwise, $\floor{\delta^{-1} \abs{x - \frac{k}{n}}} \leq \delta^{-2} \abs{x - \frac{k}{n}}^{2}$. To obtain the last equality, we expand the squares and recognise moments of a binomial random variable.

Choosing $\delta^{2} = x(1 - x) / n$, we find
$$\abs{f(x) - B_{n}(f)(x)} \leq 2 \omega\left(f, \sqrt{\frac{x (1 - x)}{n}}\right) \leq 2 \omega\left(f, \frac{1}{2 \sqrt{n}}\right).$$
Choosing $\delta = 1 / \sqrt{n}$, we also find
$$\abs{f(x) - B_{n}(f)(x)} \leq (1 + x(1 - x)) \omega\left(f, \frac{1}{\sqrt{n}}\right) \leq \frac{5}{4} \omega\left(f, \frac{1}{\sqrt{n}}\right).$$

\backtonotes