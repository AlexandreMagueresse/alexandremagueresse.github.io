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

\proposition{
Let $(u_{n})$ be a sequence taking values in a normed vector space. If $(u_{n})$ converges, then its averages converge to the same limit:
$$\lim_{n \to \infty} \frac{1}{n} \sum_{k = 1}^{n} u_{k} = \lim_{n \to \infty} u_{n}.$$
}

\proof{
Let $(V, \norm{\cdot})$ denote the underlying normed vector space and $\ell \in V$ denote the limit of $(u_{n})$. Let $\eps > 0$ be fixed. Since $(u_{n})$ converges to $\ell$, there exists $N_{\eps} \geq 0$ such that $\norm{u_{n} - \ell} \leq \eps / 2$ for all $n \geq N_{\eps}$. For all $n \geq N_{\eps}$, we have
$$\norm{\frac{1}{n} \sum_{k = 1}^{n} u_{k} - \ell} \leq \frac{1}{n} \sum_{k = 1}^{N_{\eps}} \norm{u_{k} - \ell} + \frac{1}{n} \sum_{k = N_{\eps} + 1}^{n} \norm{u_{k} - \ell} \leq \frac{S_{\eps}}{n} + \frac{1}{2} \frac{n - N_{\eps}}{n} \eps,$$
where $S_{\eps} = \sum_{k = 1}^{N_{\eps}} \norm{u_{k} - \ell}$ is independent of $n$. Since $S_{\eps} / n \to 0$, there exists $N_{\eps}' \geq 1$ such that $S_{\eps} / n \leq \eps / 2$ for all $n \geq N_{\eps}'$. Observing that $(n - N_{\eps}) / n \leq 1$, we conclude that $\norm{\frac{1}{n} \sum_{k = 1}^{n} u_{k} - \ell} \leq \eps$ for all $n \geq \max(N_{\eps}, N_{\eps}')$.
}

Note that Césaro's lemma also holds for sequences taking values in the extended real line $\overline{\RR} \doteq \RR \cup \{-\infty, +\infty\}$.

\proof{
Suppose $(u_{n})$ converges to $+\infty$. For all $A > 0$, there exists $N_{A} \geq 1$ such that $u_{n} \geq 4 A$ for all $n \geq N_{A}$. Then,
$$\frac{1}{n} \sum_{k = 1}^{n} u_{k} = \frac{1}{n} \sum_{k = 1}^{N_{A}} u_{k} + \frac{1}{n} \sum_{k = N_{A}+1}^{n} u_{k} \geq \frac{S_{A}}{n} + 4 \frac{n - N_{A}}{n} A,$$
where $S_{A} = \sum_{k = 1}^{N} u_{k}$ is independent on $n$. Since $S_{A} / n \to 0$, there exists $N_{A}' \geq 1$ such that $S_{A} / n \geq -A$ for all $n \geq N_{A}'$. Since $(n - N_{A}) / n \to 1$, there exists $N_{A}'' \geq 1$ such that $(n - N_{A}) / n \geq 1/2$ for all $n \geq N_{A}''$. Choosing $n \geq \max(N_{A}, N_{A}', N_{A}'')$, we find $\frac{1}{n} \sum_{k = 1}^{n} u_{k} \geq A$, so the averages of $(u_{n})$ converge to $+\infty$.

The same reasoning applies if $(u_{n})$ converges to $-\infty$.
}

## Converse
It is natural to ask whether there exists a converse to Cesàro's lemma: if the averages of a sequence converge, does the sequence itself converge? This cannot be true without further asumptions: taking $u_{n} = (-1)^{n}$, the Cesàro averages converge to $0$, but $(u_{n})$ does not converge.

In the case of real-valued sequences, a simple converse is the following.
\proposition{
Suppose $(u_{n})$ is a monotonous, real-valued sequence such that its averages converge. Then $(u_{n})$ converges to the same limit as its averages:
$$\lim_{n \to \infty} u_{n} = \lim_{n \to \infty} \frac{1}{n} \sum_{k = 1}^{n} u_{k}.$$
}

\proof{
By the monotone convergence theorem for real-valued sequences, we infer that $(u_{n})$ converges to some $\ell \in \overline{\RR}$. By Cesàro's lemma, the averages of $(u_{n})$ also converge to $\ell$.
}

With a stronger assumption, one can show the following converse, known as the weak version of Hardy's theorem. Morally, if the averages of a sequence converge and the successive terms of the sequence accumulate increasingly fast, then the sequence converges.

\proposition{
Let $(u_{n})$ be a sequence that takes values in a normed vector space. Suppose that the averages of $(u_{n})$ converge to $\ell$ and that $(u_{n+1} - u_{n}) = o(1/n)$. Then $(u_{n})$ converges to $\ell$.
}

\proof{
Introduce $v_{1} = u_{1}$ and $v_{n} = u_{n} - u_{n-1}$. Then rewrite
$$\begin{align*}
u_{n} - \frac{1}{n} \sum_{k = 1}^{n} u_{k} &= \sum_{j = 1}^{n} v_{j} - \frac{1}{n} \sum_{k = 1}^{n} \sum_{j = 1}^{k} v_{j} \\
&= \sum_{j = 1}^{n} v_{j} - \frac{1}{n} \sum_{j = 1}^{n} \sum_{k = j}^{n} v_{j} \\
&= \sum_{j = 1}^{n} v_{j} - \frac{1}{n} \sum_{j = 1}^{n} (n - j + 1) v_{j} \\
&= \frac{1}{n} \sum_{j = 1}^{n} (j - 1) v_{j}.
\end{align*}$$
We have assumed $(j - 1) v_{j} \to 0$, so by Cesàro's lemma, we infer $\frac{1}{n} \sum_{j = 1}^{n} (j - 1) v_{j} \to 0$.

Let $\eps > 0$. By the above, there exists $N_{\eps} \geq 1$ such that $\norm{u_{n} - \frac{1}{n} \sum_{k = 1}^{n} u_{k}} \leq \eps / 2$ for all $n \geq N_{\eps}$. Since the averages of $(u_{n})$ converge to $\ell$, there exists $N_{\eps}'$ such that $\norm{\frac{1}{n} \sum_{k = 1}^{n} u_{k} - \ell} \leq \eps / 2$ for all $n \geq N_{\eps}'$. We conclude that
$$\norm{u_{n} - \ell} \leq \norm{u_{n} - \frac{1}{n} \sum_{k = 1}^{n} u_{k}} + \norm{\frac{1}{n} \sum_{k = 1}^{n} u_{k} - \ell} \leq \eps$$
for all $n \geq \max(N_{\eps}, N_{\eps}')$.
}

Hardy's theorem has a stronger version that only requires that the successive terms accumulate at a rate $1/n$.

\proposition{
Let $(u_{n})$ be a sequence that takes values in a normed vector space. Suppose that the averages of $(u_{n})$ converge to $\ell$ and that $(u_{n+1} - u_{n}) = O(1/n)$. Then $(u_{n})$ converges to $\ell$.
}

\proof{
Define $v_{n} = u_{n+1} - u_{n}$. Let $m > n > 1$. We compute
$$\begin{align*}
\frac{\sum_{k = n+1}^{m} u_{k}}{m - n} - u_{n} &= \frac{1}{m - n} \sum_{k = n+1}^{m} (u_{k} - u_{n}) \\
&= \frac{1}{m - n} \sum_{k = n+1}^{m} \sum_{j = n}^{k - 1} (u_{j+1} - u_{j}) \\
&= \frac{1}{m - n} \sum_{k = n+1}^{m} \sum_{j = n}^{k - 1} v_{j} \\
&= \frac{1}{m - n} \sum_{j = n}^{m - 1} \sum_{k = j+1}^{m} v_{j} \\
&= \sum_{j = n}^{m - 1} \frac{m - j}{m - n} v_{j}.
\end{align*}$$
Since $u_{n+1} - u_{n} = O(1/n)$, we infer that there exists $K > 0$ such that $v_{j} \leq K / j$. Therefore
$$\frac{\sum_{k = n+1}^{m} u_{k}}{m - n} - u_{n} \leq \sum_{j = n}^{m - 1} \frac{m - j}{m - n} \frac{K}{j} \leq K \sum_{j = n + 1}^{m - 1} \frac{1}{j} \leq K \ln\left(\frac{m - 1}{n}\right),$$
where we used $1/j \leq \ln(j) - \ln(j-1)$, and the fact that the term corresponding to $j = n$ is zero. Introduce $a_{n} = \frac{1}{n} \sum_{k = 1}^{n} u_{k}$ such that $(a_{n})$ converges to $\ell$. We now decompose
$$\begin{align*}
\norm{u_{n} - \ell} & \leq \norm{u_{n} - \frac{\sum_{k = n+1}^{m} u_{k}}{m - n}} + \norm{\frac{\sum_{k = n+1}^{m} u_{k}}{m - n} - \ell} \\
& \leq K \ln\left(\frac{m - 1}{n}\right) + \norm{\frac{m a_{m} - n a_{n}}{m - n} - \ell} \\
& \leq K \ln\left(\frac{m - 1}{n}\right) + \frac{m}{m - n} \norm{a_{m} - \ell} + \frac{n}{m - n} \norm{a_{n} - \ell}.
\end{align*}$$
Choose $m(n) = 1 + \floor{\gamma n}$ for some $\gamma > 1$, so that the first term is bounded by $K \ln \gamma$. Now let $\eps > 0$ and choose $\gamma_{\eps}$ such that $K \ln \gamma_{\eps} \leq  \eps / 2$. Let $\alpha_{\eps} > 0$. Since $(a_{n}) \to \ell$, there exists $N_{\eps}$ such that $\norm{a_{n} - \ell} \leq \alpha_{\eps} \eps$ for all $n \geq N_{\eps}$, and therefore
$$\norm{u_{n} - \ell} \leq \left(\frac{1}{2} + \alpha_{\eps} \frac{m(n) + n}{m(n) - n}\right) \eps \leq \left(\frac{1}{2} + \alpha_{\eps} \frac{(\gamma_{\eps} + 1) n + 1}{(\gamma_{\eps} - 1) n}\right) \eps \leq \left(\frac{1}{2} + \alpha_{\eps} \frac{\gamma_{\eps} + 2}{\gamma_{\eps} - 1}\right) \eps,$$
where we used $n \geq 1$ to obtain the last inequality. Choosing $\alpha_{\eps} = (\gamma_{\eps} - 1) / (2 (\gamma_{\eps} + 2))$, we reach $\norm{u_{n} - \ell} \leq \eps$ for all $n \geq N_{\eps}$. 
}

## Application
Cesàro's lemma is very useful when applied to telescoping sequences. If $(u_{n})$ converges to $0$, it is sometimes easy to show that the sequence $(v_{n})$ defined by $v_{n} \doteq u_{n+1}^{\alpha} - u_{n}^{\alpha}$ converges to a finite and non-zero limit $\ell$ for some appropriate choice of $\alpha < 0$. Cesàro's lemma then provides
$$
\frac{1}{n} (u_{n}^{\alpha} - u_{0}^{\alpha}) = \frac{1}{n} \sum_{k = 0}^{n - 1} v_{k} \to \ell,
$$
which shows that $u_{n}^{\alpha} \sim \ell n$; that is, $u_{n} \sim (\ell n)^{1/\alpha}$. Importantly, Cesaro's lemma is used in the method of small steps, see [this note](/notes/small_steps).

More generally, if there exists a function $f: \RR \to \RR$ such that $v_{n} \doteq f(u_{n+1}) - f(u_{n})$ converges to $\ell \in \RR \backslash \{0\}$, then the same method shows $f(u_{n}) / n \sim \ell$.

If $(u_{n})$ is positive and $u_{n+1} / u_{n} \to \ell$, then taking $f = \ln$ shows $\ln(u_{n}) \sim \ln(\ell) n$, therefore $\ln(u_{n}) / n \sim \ln(\ell)$. Composing by the exponential, we reach $u_{n}^{1/n} \sim \ell$.

\backtonotes