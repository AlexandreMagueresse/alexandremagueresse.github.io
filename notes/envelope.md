+++
title = "Envelope of a family of curves"
hasmath = true
hascode = false
date = Date(2025, 06, 13)

rss_title = "Envelope of a family of curves"
rss_description = "Envelope of a family of curves"
rss_pubdate = Date(2025, 06, 13)

tags = ["research"]
+++

\backtonotes

# Envelope of a family of curves

\definition{Envelope}{
The **envelope** of a family of planar curves is a curve that is tangent, at each of its points, to a member of the family.
}

Suppose we are given a family of curves described by
$$C_{t} = \{(x, y) \in \RR^{2}, f_{t}(x, y) = 0\}$$
for all $t \in \RR$. For convenience, consider the function $F: (t, x, y) \mapsto f_{t}(x, y)$ and assume $F$ is differentiable. A point $(x, y) \in \RR^{2}$ belongs to the envelope of the family $(C_{t})$, if and only if there exists $t \in \RR$ such that
$$F(t, x, y) = \partial_{t} F(t, x, y) = 0$$
simultaneously.

An important and easy special case is when the family of curves are lines. Suppose $f_{t}(x, y) = a(t) x + b(t) y - c(t)$ for some differentiable functions $a, b, c: \RR \to \RR$. A point $(x, y) \in \RR^{2}$ belongs to the envelope if there exists $t \in \RR$ such that
$$a(t) x + b(t) y = c(t), \qquad a'(t)  x + b'(t) y = c'(t).$$
This is a linear system in $(x, y)$, which we can solve if it is not singular, that is, if $a(t) b'(t) \neq a'(t) b(t)$. In that case, we find
$$(x, y) = \left(\frac{b' c - b c'}{a b' - a' b}, \frac{a' c - a c'}{a' b - a b'}\right),$$
where we omitted the parameter $t$ for cleaner notations.

\example{
    Let $k \geq 1$ and consider connecting the lines connecting the complex points $e^{i t}$ and $e^{k i t}$, for all $t \in \co{0}{2\pi}$. The equation of these lines correspond to the coefficients $a(t) = \sin(k t) - \sin(t)$, $b(t) = \cos(t) - \cos(k t)$ and $c(t) = \sin((k - 1) t)$. Noticing that $a$ and $b$ can be factored by $\sin([(k - 1) / 2] t)$, we are left with new coefficients $A(t) = \cos([(k+1)/2] t)$, $B(t) = \sin([(k+1)/2] t)$ and $C(t) = \cos([(k-1)/2] t)$ after simplifying. Applying the parameterisation of the envelope established above, we obtain
    $$\begin{align*}
    x(t) &= \cos\left(\frac{k+1}{2}t\right) \cos\left(\frac{k-1}{2} t\right) + \frac{k-1}{k+1} \sin\left(\frac{k+1}{2} t\right) \sin\left(\frac{k-1}{2}t\right), \\
    y(t) &= \sin\left(\frac{k+1}{2}t\right) \cos\left(\frac{k-1}{2} t\right) - \frac{k-1}{k+1} \cos\left(\frac{k+1}{2} t\right) \sin\left(\frac{k-1}{2}t\right),
    \end{align*}$$
    which simplifies into
    $$\begin{align*}
    x(t) &= \frac{1}{k+1} [k \cos(t) + \cos(kt)], \\
    y(t) &= \frac{1}{k+1} [k \sin(t) + \sin(kt)].
    \end{align*}$$
    This is the equation of an epicycloid; it can also be obtained by rolling (without slipping) a small circle of radius $1/(k+1)$ around a circle of radius $1 - 2/(k+1)$.
}