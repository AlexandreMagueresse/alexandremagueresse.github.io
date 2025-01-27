+++
title = "Cesàro's lemma"
hasmath = true
hascode = false
date = Date(2025, 01, 27)

rss_title = "Cesàro's lemma"
rss_description = "Cesàro's lemma"
rss_pubdate = Date(2025, 01, 27)

tags = ["research"]
+++

\backtonotes

# Cesàro's lemma

@@proposition
Suppose the sequence $(u_{n})$ converges. Then
$$\lim_{n \to \infty} \frac{1}{n} \sum_{k = 1}^{n} u_{k} = \lim_{n \to \infty} u_{n}.$$
@@

## Proof
Let $\ell$ denote the limit of $u_{n}$ and $\eps > 0$. There exists $N \geq 0$ such that $\abs{u_{n} - \ell} \leq \eps$ for all $n \geq N$. Let $n \geq N$. We have
$$\abs{\frac{1}{n} \sum_{k = 1}^{n} u_{k} - \ell} \leq \abs{\frac{1}{n} \sum_{k = 1}^{N} (u_{k} - \ell)} + \abs{\frac{1}{n} \sum_{k = N + 1}^{n} (u_{k} - \ell)} \leq \frac{K}{n} + \frac{n - N}{n} \eps \leq \frac{K}{n} + \eps,$$
where $K = \abs{\sum_{k = 1}^{N} (u_{k} - \ell)}$. Choosing $n \geq K / \eps$ ensures that $\abs{\frac{1}{n} \sum_{k = 1}^{n} u_{k} - \ell} \leq 2 \eps$.

## Example
Note that the converse is not true. For example, taking $u_{n} = (-1)^{n}$, the Cesàro averages converge to $0$, but $(u_{n})$ does not converge. However, taking $v_{n} = \sum_{k = 0}^{n} u_{k}$, we easily see that $v_{2n} = 1$ and $v_{2n+1} = 0$. The sequence $(v_{n})$ does not converge, but the associated Cesàro mean does:
$$
\frac{1}{n} \sum_{k = 0}^{n - 1} v_{n} = \frac{\floor{(n + 1) / 2}}{n} \to \frac{1}{2}.
$$
Cesàro's lemma is very useful when applied to telescoping sequences. If $u_{k}$ converges to $0$, it is sometimes easy to show that $v_{k} \doteq u_{k+1}^{\alpha} - u_{k}^{\alpha}$ converges to a non-zero limit $\ell$ for some appropriate choice of $\alpha < 0$. Cesàro's lemma then provides
$$
\frac{1}{n} (u_{n}^{\alpha} - u_{0}^{\alpha}) = \frac{1}{n} \sum_{k = 0}^{n - 1} v_{k} \to \ell,
$$
which shows that $u_{n}^{\alpha} \sim \ell n$; that is, $u_{n} \sim (\ell n)^{1/\alpha}$. Importantly, Cesaro's lemma is used in the method of small steps, see [this note](/notes/small_steps).

\backtonotes