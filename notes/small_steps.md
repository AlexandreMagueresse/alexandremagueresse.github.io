+++
title = "Method of small steps"
hasmath = true
hascode = false
date = Date(2025, 01, 27)

rss_title = "Method of small steps"
rss_description = "Method of small steps"
rss_pubdate = Date(2025, 01, 27)

tags = ["research"]
+++

\backtonotes

# Method of small steps

\proposition{
Let $z \in \RR$ and $h > 0$. Suppose $f \in C^{0}(\oo{z - h}{z + h}, \RR)$ is such that $f$ has a series expansion around $z$ of the shape
$$
f(z + x) = z + x - \alpha x \abs{x}^{p} + \beta x \abs{x}^{p + q} + o(\abs{x}^{p + q + 1}),
$$
where $\alpha, \beta, p, q > 0$. Provided $x_{0} \in \RR$ is close to $z$, the sequence defined by $x_{k+1} = f(x_{k})$ converges to $z$ and
$$
\abs{x_{n} - z} = \left\{\begin{array}{ll}
\displaystyle \frac{1}{(\alpha p n)^{1/p}} + \frac{\beta p}{(p - q) (\alpha p)^{(p + q + 1)/p}} \frac{1}{n^{1+q/p}} + o\left(\frac{1}{n^{1+q/p}}\right) & \text{if } q < p, \\
\displaystyle \frac{1}{(\alpha p n)^{1/p}} - \frac{\alpha^{2} (p + 1) - 2 \beta}{2 (\alpha p)^{2 + 1/p}} \frac{\ln n}{n^{1 + 1/p}} + o\left(\frac{\ln n}{n^{1 + 1/p}}\right) & \text{if } q = p, \\
\displaystyle \frac{1}{(\alpha p n)^{1/p}} - \frac{\alpha^{2} (p + 1)}{2 (\alpha p)^{2 + 1/p}} \frac{\ln n}{n^{1 + 1/p}} + o\left(\frac{\ln n}{n^{1 + 1/p}}\right) & \text{if } q > p.
\end{array}\right.
$$
The result for the case $q = p$ is subject to $\alpha^{2} (p + 1) \neq 2 \beta$.
}

\proof{
Let $x_{0} \in \RR$ and introduce the sequence $y_{k} = x_{k} - z$. Then $(y_{k})$ satisfies the recursion
$$
y_{k+1} = f(z + y_{k}) - z = g(y_{k}),
$$
where we have introduced $g \in C^{0}(\oo{-h}{h}, \RR)$ defined by $g(x) = f(z + x) - z$. 

### Step 1: Good definition and convergence of $(y_{k})$
Since $g$ is only defined on $\oo{-h}{h}$, we need to show that the sequence $(y_{k})$ is well-defined; that is, under appropriate assumptions on $x_{0}$, the iterates $(y_{k})$ remain in (a subset of) $\oo{-h}{h}$.

We first observe that the series expansion of $f$ around $z$ is equivalent to the series expansion of $g$ around $0$ given by
$$
g(x) = x - \alpha x \abs{x}^{p} + \beta x \abs{x}^{p + q} + o(\abs{x}^{p + q + 1}).
$$

One can write $g(x) = x \ell(x)$ and $x - g(x) = \alpha x \abs{x}^{p} m(x)$ where $\ell, m: \oo{-h}{h} \to \RR$ tend to $1$ when $x \to 0$. In particular, there exists $\delta \in \oo{0}{h}$ such that $\ell$ and $m$ are positive in $\cc{-\delta}{\delta}$. We now separate two cases:
* When $x \in \oc{0}{\delta}$, we infer that $g(x) > 0$ and $g(x) - \alpha x < 0$. Rearranging, this gives $0 < g(x) < \alpha x \leq x \leq \delta$. In other words, the interval $\oc{0}{\delta}$ is stable by $g$. Assuming $y_{k} \in \oc{0}{\delta}$ for some $k \geq 0$ ensures that $g$ can be evaluated at $y_{k}$, so $y_{k+1}$ is well defined. By induction, choosing $y_{0} \in \oc{0}{\delta}$ ensures that $(y_{k})$ is well defined and $y_{k} \in \oc{0}{\delta}$ for all $k \geq 0$. Next, the inequality $g(x) < x$ implies that $(y_{k})$ is decreasing. Besides, $(y_{k})$ is also bounded from below (by $0$), so $(y_{k})$ converges to some $y_{\infty} \in \cc{0}{\delta}$. Since $g$ is continuous, we know that $y_{\infty}$ is a fixed point of $g$. The inequality $g(x) < x$ in $\oc{0}{\delta}$ implies that $y_{\infty} = 0$.
* When $x \in \co{-\delta}{0}$, a similar reasoning as above proves that $\co{-\delta}{0}$ is stable by $g$, that $(y_{k})$ is increasing and bounded from above by $0$. Analogous arguments show that $(y_{k})$ converges to $0$.

In both cases, $(y_{k})$ converges to $0$ provided that $y_{0} \in \cc{-\delta}{\delta}$; that is $x_{0} \in \cc{z - \delta}{z + \delta}$. Since $x_{k} = z + y_{k}$, the existence of $(y_{k})$ implies that of $(x_{k})$, and we also have $x_{k} \in \cc{z - \delta}{z + \delta}$, and $(x_{k})$ converges to $z$.

### Step 2: Equivalent of $(y_{k})$

Let $\lambda \in \RR$ and define $u_{k} = \abs{y_{k+1}}^{\lambda} - \abs{y_{k}}^{\lambda}$ for all $k \geq 1$. Since $g(y_{k})$ and $y_{k}$ have the same sign, we compute
$$
\label{expansion}
\begin{align*}
u_{k} &= \abs{y_{k} - \alpha y_{k} \abs{y_{k}}^{p} + \beta y_{k} \abs{y_{k}}^{p + q} + o(\abs{y_{k}}^{p + q + 1})}^{\lambda} - \abs{y_{k}}^{\lambda} \\
&= \abs{y_{k}}^{\lambda} \left(\left(1 - \alpha \abs{y_{k}}^{p} + \beta \abs{y_{k}}^{p + q} + o(\abs{y_{k}}^{p + q})\right)^{\lambda} - 1\right) \\
&= \abs{y_{k}}^{\lambda} \left(- \lambda \alpha \abs{y_{k}}^{p} + \lambda \beta \abs{y_{k}}^{p + q} + \frac{\lambda (\lambda - 1)}{2} \alpha^{2} \abs{y_{k}}^{2 p} + o(\abs{y_{k}}^{p + \min(p, q)})\right).
\end{align*}
$$
Since $(y_{k})$ tends to $0$ and $\min(p, q) > 0$, choosing $\lambda = -p$ makes $u_{k}$ converge to $-\lambda \alpha = \alpha p$. By Cesàro's lemma (see [this note](/notes/cesaro)), we infer that $\abs{y_{k}}^{-p} \sim \alpha p k$.

### Step 3: Expansion of $(y_{k})$

We rewrite \eqref{expansion} when $\lambda = -p$ and depending on the value of $q$:
$$
u_{k} = \alpha p + C_{p, q} \abs{y_{k}}^{\min(p, q)}(1 + o(1)), \qquad C_{p, q} = \left\{\begin{array}{ll}
\displaystyle - \beta p & \text{if } q < p, \\
\displaystyle \alpha^{2} \frac{p (p + 1)}{2} - \beta p & \text{if } q = p, \\
\displaystyle \alpha^{2} \frac{p (p + 1)}{2} & \text{if } q > p.
\end{array}\right.
$$
The equality for the case $q = p$ is only true when $C_{p, p} \neq 0$, that is when $\alpha^{2} (p + 1) \neq 2 \beta$. Summing $(u_{k})$ between $k = 1$ and $k = n - 1$ for some $n \geq 1$, we obtain
$$
\abs{y_{n}}^{-p} - \abs{y_{1}}^{-p} = \alpha p n + C_{p, q} \sum_{k = 1}^{n - 1} \abs{y_{k}}^{\min(p, q)} (1 + o(1)).
$$
We have established $\abs{y_{k}}^{-p} \sim \alpha p k$ in the previous step, so $\abs{y_{k}}^{\min(p, q)} \sim (\alpha p k)^{-\min(1, q/p)}$. Since the series of term $k^{-\min(1, q/p)}$ diverges, we can use the equivalence of the partial sums to infer
$$
\sum_{k = 1}^{n - 1} \abs{y_{k}}^{\min(p, q)} \sim \sum_{k = 1}^{n - 1} (\alpha p k)^{-\min(1, q/p)} = (\alpha p)^{-\min(1, q/p)} \sum_{k = 1}^{n - 1} k^{-\min(1, q/p)} \sim \left\{\begin{array}{ll}
\displaystyle (\alpha p)^{-q/p} \frac{n^{1 - q/p}}{1 - q/p} & \text{if } q < p, \\
\displaystyle (\alpha p)^{-1} \ln n & \text{if } p \leq q
\end{array}\right.
$$
Plugging this equivalent, and carefully raising to the power $-1/p$, we conclude
$$
\abs{x_{n} - z} = \left\{\begin{array}{ll}
\displaystyle \frac{1}{(\alpha p n)^{1/p}} + \frac{\beta p}{(p - q) (\alpha p)^{(p + q + 1)/p}} \frac{1}{n^{1+q/p}} + o\left(\frac{1}{n^{1+q/p}}\right) & \text{if } q < p, \\
\displaystyle \frac{1}{(\alpha p n)^{1/p}} - \frac{\alpha^{2} (p + 1) - 2 \beta}{2 (\alpha p)^{2 + 1/p}} \frac{\ln n}{n^{1 + 1/p}} + o\left(\frac{\ln n}{n^{1 + 1/p}}\right) & \text{if } q = p, \\
\displaystyle \frac{1}{(\alpha p n)^{1/p}} - \frac{\alpha^{2} (p + 1)}{2 (\alpha p)^{2 + 1/p}} \frac{\ln n}{n^{1 + 1/p}} + o\left(\frac{\ln n}{n^{1 + 1/p}}\right) & \text{if } q > p.
\end{array}\right.
$$
}

## Example
Let $u_{0} \in \RR$ and define $(u_{k})$ via
$$
u_{k+1} = \sin(u_{k}).
$$
Since $\sin(x) = x - \frac{1}{3!} x^{3} + \frac{1}{5!} x^{5} + o(x^{5})$, we can apply the result above with $z = 0$, $\alpha = 1/6$, $\beta = 1/120$, $p = 2$ and $q = 2$. We then have
$$\abs{u_{n}} = \sqrt{\frac{3}{n}} \left(1 - \frac{3 \ln n}{10 n}\right) + o\left(\frac{\ln n}{n \sqrt{n}}\right).$$
In this case, $0$ is the only fixed point of $\sin$ and $\sin$ is bounded, so this estimate is valid for all initialisations.

\backtonotes