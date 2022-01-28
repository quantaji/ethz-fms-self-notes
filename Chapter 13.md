# Asymptotics

## Exams
- concept of convergence, know all definition
    - Almost sure convergence
    - Convergence in probability 
    - Convergence in distribution 
- Stochastic order symbols
    - question involve stochastic order symbol, should know what they mean 
- CLT (need to know)
- Slutsky’s Thm + proof 
- Consistency 
- Asymptotic normality 
- Asymptotic linearity 
- δ-technique

## 13.1 Type of convergence
1. Convergence almost surely
   1. Definition: Given a probability space $(\Omega,\mathcal{F},\mathbb{P})$, we have a sereis of random variable $\{X_n(\omega);n\in\mathbb{N},\omega\in\Omega\}$, and a random variable $X(\omega)$, we consider the invent of $A_X = \left\{ \omega;\lim_{n\to\infty}X_n(\omega) = X(\omega) \right\}$, if $\mathbb{P}(A_X) = 1$, then we call random variable $X_{n}$ converge to random variable $X$ almost surely, or $X_{n}\overset{a.s.}{\to}X$.
   2. There is strong correlation of $X_{n}$ and $X$, since they are all controlled by $\omega$.
2. Convergence in probability
   1. Definition: Given a probability space $(\Omega,\mathcal{F},\mathbb{P})$, we have a sereis of random variable $\{X_n(\omega);n\in\mathbb{N},\omega\in\Omega\}$, and a random variable $X(\omega)$. If forall $\epsilon>0$, we have ``\lim_{n\to\infty}\mathbb{P}\left( ||X_n(\omega) - X(\omega)|| > \epsilon \right) = 0``, then we call random variable $X_{n}$ converge to random variable $X$ in probability, or $X_{n}\overset{\mathbb{P}}{\to}X$. 
3. Convergence in distribution
   1. Definition: Let $X_{n}$ and $X$ be random variables, let $f$ be an arbitary bounded and continuous function, if $\lim_{n\to\infty}\mathbb{E}[f(X_n)] = \mathbb{E}[f(X)]$, then we say $X_n$ converge to $X$ in probability, or $X_{n}\overset{\mathcal{D}}{\to} X$.
   2. This is the weakest form of convergence, there is no correlation b.t.w. $X_n$ and $X$, just here distribution function.
   3. An example of this is the central limit theorem
4. $\mathrm{L}^{p}$-Convergence
    1. Definition: Given a probability space $(\Omega,\mathcal{F},\mathbb{P})$, we have a sereis of random variable $\{X_n(\omega);n\in\mathbb{N},\omega\in\Omega\}$, and a random variable $X(\omega)$. If ``\lim_{n\to\infty} \mathbb{E}\left[ |X_n(\omega) - X(\omega)|^p \right] = 0``, then we call random variable $X_{n}$ converge in $L^p$ to random variable $X$. 

### Properties Set 1 (from Wkipeida)
Provided the probability space is *complete*:
* If ``X_n\ \xrightarrow{\overset{}{\mathbb{P}}}\ X`` and ``X_n\ \xrightarrow{\overset{}{\mathbb{P}}}\ Y``, then ``X=Y`` almost surely.
* If ``X_n\ \xrightarrow{\overset{}{\mathrm{a.s.}}}\ X`` and ``X_n\ \xrightarrow{\overset{}{\mathrm{a.s.}}}\ Y``, then ``X=Y`` almost surely.
* If ``X_n\ \xrightarrow{\overset{}{L^r}}\ X`` and ``X_n\ \xrightarrow{\overset{}{L^r}}\ Y``, then ``X=Y`` almost surely.
* If ``X_n\ \xrightarrow{\overset{}{\mathbb{P}}}\ X`` and ``Y_n\ \xrightarrow{\overset{}{\mathbb{P}}}\ Y``, then ``aX_n+bY_n\ \xrightarrow{\overset{}{\mathbb{P}}}\ aX+bY`` (for any real numbers {{mvar|a}} and {{mvar|b}}) and ``X_n Y_n\xrightarrow{\overset{}{\mathbb{P}}}\ XY``.
* If ``X_n\ \xrightarrow{\overset{}{\mathrm{a.s.}}}\ X`` and ``Y_n\ \xrightarrow{\overset{}{\mathrm{a.s.}}}\ Y``, then ``aX_n+bY_n\ \xrightarrow{\overset{}{\mathrm{a.s.}}}\ aX+bY`` (for any real numbers {{mvar|a}} and {{mvar|b}}) and ``X_n Y_n\xrightarrow{\overset{}{\mathrm{a.s.}}}\ XY``.
* If ``X_n\ \xrightarrow{\overset{}{L^r}}\ X`` and ``Y_n\ \xrightarrow{\overset{}{L^r}}\ Y``, then ``aX_n+bY_n\ \xrightarrow{\overset{}{L^r}}\ aX+bY`` (for any real numbers {{mvar|a}} and {{mvar|b}}).
* None of the above statements are true for **convergence in distribution**.

### Properties Set 2
$$
\begin{matrix}
        X_n \xrightarrow{\overset{}{L^s}} X & \underset{s>r\geq1}{\Rightarrow} & X_n \xrightarrow{\overset{}{L^r}}  X &                 &                             \\
                                            &                                  & \Downarrow                           &                 &                             \\
        X_n \xrightarrow{\mathrm{a.s.}} X   & \Rightarrow                      & X_n \xrightarrow{\mathbb{P}}    X    &  \Rightarrow & X_n \xrightarrow{\mathcal{D}} X
\end{matrix}
$$
1. ``X_{n} \stackrel{\text { a.s. }}{\longrightarrow} X  \Rightarrow  X_{n} \stackrel{\mathbb{P}}{\rightarrow} X``.
    1. Proof of "$\Rightarrow$": 
         1. Rewrite $A_X$  as ``A_{X,\epsilon} = \{ \omega; \exists N(\omega), \forall n>N(\omega), ||X_n(\omega) - X(\omega)|| < \epsilon\}``. $X_n\overset{a.s.}{\to}X$ means $\mathbb{P}(A_{X,\epsilon}) = 1,\forall \epsilon$. 
         2. The counter set of $A_{X,\epsilon}$ is ``A_{X,\epsilon}^c = \{\omega; \forall n,\exists N(\omega) \geq n, ||X_{N(\omega)}(\omega) - X(\omega)|| \geq \epsilon\} = \cap_{n=0}^{\infty}\left( \cup_{m \geq n} \{\omega; ||X_{m}(\omega) - X(\omega)|| \geq \epsilon\} \right)``. 
         3. If we define ``C_{n,\epsilon} := \{ \omega; ||X_n(\omega) - X(\omega)|| > \epsilon \}`` and $B_{n,\epsilon} := \cup_{m\geq n}C_{n,\epsilon}$, then $A_{X,\epsilon}^c = \cap_{n=0}^{\infty}B_{n,\epsilon}$. The claim we want to prove is that $\lim_{n\to\infty} \mathbb{P}(C_{n,\epsilon}) = 0,\forall \epsilon$. We can bound it with $\mathbb{P}(C_{n,\epsilon}) \leq \mathbb{P}(B_{n,\epsilon})$
         4. Since $B_{n,\epsilon}\supset B_{n+1,\epsilon}$ for all $n$. We can conclude that $\lim_{n\to\infty}P(B_{n,\epsilon}) = \mathbb{P}(A_{X,\epsilon}^c)$. Since $\mathbb{P}(A_{X,\epsilon})=1$ then $\mathbb{P}(A_{X,\epsilon}^c)=0$ therefore $\lim_{n\to\infty}\mathbb{P}(C_{n,\epsilon}) = 0,\forall \epsilon$.
     1. Counter Example of "$\Leftarrow$": (from wikipedia)
         1. Consider $\omega\in[0,1)$.
         2. $X_1 = 1_{\{ \omega \in [0,1) \}}$
         3. $X_2 = 1_{\{ \omega \in [0,1/2) \}}$,$X_3 = 1_{\{ \omega \in [1/2,1) \}}$
         4. $X_4 = 1_{\{ \omega \in [0,1/4) \}}$,$X_5 = 1_{\{ \omega \in [1/4,1/2) \}}$,$X_6 = 1_{\{ \omega \in [1/2,3/4) \}}$,$X_7 = 1_{\{ \omega \in [3/4,1) \}}$
         5. $\forall(k, m) \in \mathbb{N}, 0 \leqslant k \leqslant 2^{m}-1, X_{2^{m}+k}=\mathbf{1}_{\left\{\omega \in\left[\frac{k}{2^{m}}, \frac{k+1}{2^{m}}\right)\right\}}$
         6. Then ``\forall 2^{m} \leqslant n \leqslant 2^{m+1}-1, \mathbb{P}\left(\left|X_{n}-0\right| \geqslant \varepsilon\right)=\frac{1}{2^{m}}``, we can see that $X_{n}$ converge to zero in probability.
         7. But for all $\omega$, we can see that for large enough $n$ there always exists $X_{n}(\omega) = 1$, therefore $\lim_{n\to\infty}X_{n}(\omega)$ does not exists for all $\omega$.
2. ``X_{n} \stackrel{\mathbb{P}}{\rightarrow} X   \Rightarrow  X_{n}\stackrel{\mathcal{D}}{\rightarrow} X`` (Proof from [Wikipedia](https://en.wikipedia.org/wiki/Proofs_of_convergence_of_random_variables#propB2))
    1. For scalar case:
        1. first prove ``\operatorname{Pr}(Y \leq a) \leq \operatorname{Pr}(X \leq a+\varepsilon)+\operatorname{Pr}(|Y-X|>\varepsilon)`` using union bound ``\{Y \leq a\} \subset\{X \leq a+\varepsilon\} \cup\{|Y-X|>\varepsilon\}``
        2. $\forall \varepsilon$, use the above lemma given $Y\leftarrow X_n, X \leftarrow X, a \leftarrow a$ and $Y\leftarrow X, X \leftarrow X_n, a \leftarrow a-\varepsilon$, we have   ``\operatorname{Pr}\left(X_{n} \leq a\right) \leq \operatorname{Pr}(X \leq a+\varepsilon)+\operatorname{Pr}\left(\left|X_{n}-X\right|>\varepsilon\right)`` and ``\operatorname{Pr}(X \leq a-\varepsilon) \leq \operatorname{Pr}\left(X_{n} \leq a\right)+\operatorname{Pr}\left(\left|X_{n}-X\right|>\varepsilon\right)``,
        3. then ``\operatorname{Pr}(X \leq a-\varepsilon)-\operatorname{Pr}\left(\left|X_{n}-X\right|>\varepsilon\right) \leq \operatorname{Pr}\left(X_{n} \leq a\right) \leq \operatorname{Pr}(X \leq a+\varepsilon)+\operatorname{Pr}\left(\left|X_{n}-X\right|>\varepsilon\right)`` and taking $n$ to infinity, we have ``F_{X}(a-\varepsilon) \leq \lim _{n \rightarrow \infty} \operatorname{Pr}\left(X_{n} \leq a\right) \leq F_{X}(a+\varepsilon)``
        4. If we assume $F_X(\cdot)$ continuous at $a$, we have ``\lim _{n \rightarrow \infty} \operatorname{Pr}\left(X_{n} \leq a\right)=\operatorname{Pr}(X \leq a)``.
3. ``X_{n} \stackrel{\mathbb{P}}{\rightarrow} X  \Rightarrow  X_{k_{n}} \stackrel{\text { a.s. }}{\longrightarrow} X``, existance of sub-sequence convergence.
4. ``X_{n} \stackrel{L^{r}}{\rightarrow} X  \Rightarrow  X_{n} \stackrel{\mathbb{P}}{\rightarrow} X``
    1. Markov inequation for a increasing function $\phi(x)$, ``\mathbb{P}(X\geq a) = \mathbb{P}(\phi(X)\geq \phi(a)) \leq \mathbb{E}[\phi(X)] / \phi(a) ``
    2. Using ``\phi(x) = x^p`` and ``X = |X_n - X|`` we can prove it.
    3. The reverse is not true, see examples [here](https://ece.iisc.ac.in/~parimal/2019/random/lecture-15.pdf).
        1. ``X_{n}(\omega)=2^{n} \mathbb{1}_{\left[0, \frac{1}{n}\right]}(\omega)`` for $\omega \in [0,1]$
        2. $X_n \overset{\mathbb{P}}{\to} 0$, but ``\mathbb{E}\left|X_{n}\right|^{p}={2^{n p}}/{n}``.
5. ``X_{n} \stackrel{L^{s}}{\longrightarrow} X \underset{s>r \geq 1}{\Rightarrow} X_{n} \stackrel{L^{r}}{\longrightarrow} X``
    1. proof using Hölder’s inequality, ``\mathbb{E}|X|^{p}=\mathbb{E}\left[|X|^{\frac{q}{q/p}} \cdot 1\right] \leqslant\left(\mathbb{E}|X|^{q}\right)^{\frac{1}{q/p}}``
6. ``X_{n} \stackrel{\mathcal{D}}{\rightarrow} c  \Rightarrow  X_{n} \stackrel{\mathbb{P}}{\rightarrow} c`` when $c$ is a constant.
7. ``X_{n} \stackrel{\mathcal{D}}{\rightarrow} X,\left|X_{n}-Y_{n}\right| \stackrel{\mathbb{P}}{\rightarrow} 0 \quad \Rightarrow \quad Y_{n} \stackrel{\mathcal{D}}{\rightarrow} X``
8. ``X_{n} \stackrel{\mathcal{D}}{\rightarrow} X, Y_{n} \stackrel{\mathcal{D}}{\rightarrow} c  \Rightarrow \left(X_{n}, Y_{n}\right) \stackrel{\mathcal{D}}{\rightarrow}(X, c)``, when $c$ is a constant.
9. ``X_{n} \stackrel{\mathbb{P}}{\rightarrow} X, Y_{n} \stackrel{\mathbb{P}}{\rightarrow} Y  \Rightarrow \left(X_{n}, Y_{n}\right) \stackrel{\mathbb{P}}{\rightarrow}(X, Y)``

### Theorem 13.1.1 Cramér-Wold device
Let ``\left(\left\{Z_{n}\right\}, Z\right)`` be a collection of $\mathbb{R}^{p}$-valued random variables. Then
```math
Z_{n} \stackrel{\mathcal{D}}{\longrightarrow} Z \Leftrightarrow a^{T} Z_{n} \stackrel{\mathcal{D}}{\longrightarrow} a^{T} Z, \forall a \in \mathbb{R}^{p} .
```
### Central Limit Theorem (CLT)
Let $X_{1}, X_{2}, \ldots$ i.i.d. copies of a random variable ``X=\left(X^{(1)}, \ldots, X^{(p)}\right)^{top}`` in $\mathbb{R}^{p}$. Assume ``\mu := \mathbb{E}X=\left(\mu_{1}, \ldots, \mu_{p}\right)^{\top}`` and ``\operatorname{Cov}(X):= \Sigma:= \mathbb{E} X X^{\top}-\mu \mu^{\top}`` exist. Define ``\bar{X}_{n}=\left(\bar{X}_{n}^{(1)}, \ldots, \bar{X}_{n}^{(p)}\right)^{\top}``, we have 
```math
\sqrt{n}\left(\bar{X}_{n}-\mu\right) \stackrel{\mathcal{D}}{\longrightarrow} \mathcal{N}(0, \Sigma)
```

### Theorem 13.1.2 Portmanteau Theorem
Let ``\left(\left\{Z_{n}\right\}, Z\right)`` be a collection of $\mathbb{R}^{p}$-valued random variables. Denote the distribution of $Z$ by $Q$ and let ``G=Q(Z \leq \cdot)`` be its distribution function. The following statements are equivalent:
1. ``Z_{n} \stackrel{\mathcal{D}}{\longrightarrow} Z`` (i.e., ``\mathbb{E} f\left(Z_{n}\right) \rightarrow \mathbb{E} f(Z) ``, ``\forall f`` bounded and continuous).
2. ``\mathbb{E} f\left(Z_{n}\right) \rightarrow \mathbb{E} f(Z) ``, ``\forall f`` bounded and *Lipschitz*. 
3. ``\mathbb{E} f\left(Z_{n}\right) \rightarrow \mathbb{E} f(Z) ``, ``\forall f`` bounded and $Q$-a.s. continuous.
    1. $f$ is *Lipschitz* if ``\exists L`` s.t. ``\|f(x)-f(\tilde{x}) \mid \leqslant L\| x-\tilde{x} \|``, ``\forall x, \tilde{x} \in \mathbb{R}^{p}``
4. ``\lim_{n\to \infty} \mathbb{P}\left(Z_{n} \leq z\right) = G(z)`` for all $G$-continuity points $z$.


### 13.1.1 stocastic order symbols
- ``Z_n`` is bounded in probability, ``Z_{n}=\mathcal{O}_{\mathbb{P}}(1)``, if ``\lim _{M \rightarrow \infty} \varlimsup _{n \rightarrow \infty} \mathbb{P}\left(\left\|Z_{n}\right\|>M\right)=0``. Also called *uniform tightness*
    - We denote ``Z_n = \mathcal{O}_{\mathbb{P}}\left(r_{n}\right)`` if ``Z_{n} / r_{n}=\mathcal{O}_{\mathbb{P}}(1)``.
- If $Z_n$ converges in probability to zero, we write this as ``Z_{n}=o_{\mathbb{P}}(1)``
    - ``Z_{n}=o_{\mathbb{P}}\left(r_{n}\right)`` ($Z_n$ is of small order $r_n$ in probability) if ``Z_{n} / r_{n}=o_{\mathbb{P}}(1)``.

### Lemma 13.1.1
- Suppose that $Z_n$ converges in distribution. Then ``Z_{n}=\mathcal{O}_{\mathbb{P}}(1)``.
- proof:
    - For scalar case, denote $Z_n \overset{\mathcal{D}}{\to} Z$, and $G(\cdot)$ the distribution function of $Z$. The proof is straightforward, ``\lim _{n \rightarrow \infty} \mathbb{P}\left(Z_{n}>M\right)=1-G(M) \leq \varepsilon``.
    - For vector case, 
        - by Cramér-Wold device we know that each component $Z_n^{(i)}\overset{\mathcal{D}}{\to} Z^{(i)}$, $\forall \varepsilon. \exists M$, s.t. $\forall i\in [p]$, ``P(|Z|^{(i)} \geq M/\sqrt{p}) < \epsilon/p``, so ``P(|Z|^{(i)} < M/\sqrt{p}) > 1 - \epsilon/p``
        - by union bound, ``P(\cup_{i\in[p]}\{ |Z|^{(i)} < M/\sqrt{p} \}) = 1 - P(\cap_{i\in[p]}\{ |Z|^{(i)} \geq M/\sqrt{p} \}) \geq 1 - \sum_{i\in[p]} P( |Z|^{(i)} \geq M/\sqrt{p} ) = 1-\varepsilon``
        - Since ``\cup_{i\in[p]}\{ |Z|^{(i)} < M/\sqrt{p} \} \subset \{ |Z| < M \}``, we have ``P(|Z| < M) \geq P(\cup_{i\in[p]}\{ |Z|^{(i)} < M/\sqrt{p} \}) \geq 1-\varepsilon``, QED.

### Theorem 13.1.3 (Slutsky’s Theorem)
- Let ``\left(\left\{Z_{n}, A_n \right\}, Z\right)`` be a collection of $\mathbb{R}^{p}$-valued random variables and ``Z_{n} \stackrel{\mathcal{D}}{\longrightarrow} Z``. Also $a\in \mathbb{R}^{p}$ is a vector of constants and ``A_{n} \stackrel{\mathbb{P}}{\longrightarrow} a``. Then ``A_{n}^{T} Z_{n} \stackrel{\mathcal{D}}{\longrightarrow} a^{T} Z``.
- Proof:
    - for any bounded Lipschitz function $f$, we have ``|f| \leq C_{B},|f(z)-f(\tilde{z})| \leq C_{L}\|z-\tilde{z}\|``,
    - Then ``\left|\mathbb{E} f\left(A_{n}^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z\right)\right|\leq \left|\mathbb{E} f\left(A_{n}^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z_{n}\right)\right| + \left|\mathbb{E} f\left(a^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z\right)\right| ``
    - For the second term, since the induced function $g(z):=f(a^{\top}z)$ is also Lipschitz, This term converge to zero.
    - For the first term, we can divide it into cases ``S_n = \left\{\left\|Z_{n}\right\| \leq M,\left\|A_{n}-a\right\| \leq \epsilon\right\}`` and its counterpart $S_n^c$,
        - by union bound, ``P(S_n^c) \leq P(\left\|Z_{n}\right\| > M) + P(\left\|A_{n}-a\right\| > \epsilon)\to 0``
    - then ``\left|\mathbb{E} f\left(A_{n}^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z_{n}\right)\right| = \left|\mathbb{E} f\left(A_{n}^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z_{n}\right)\right| 1\left\{S_{n}\right\} + \left|\mathbb{E} f\left(A_{n}^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z_{n}\right)\right| 1\left\{S^c_{n}\right\}``
        - for the first term, by Lipschitz condition ``\left|\mathbb{E} f\left(A_{n}^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z_{n}\right)\right| 1\left\{S_{n}\right\} \leq   C_L  \mathbb{E}|(A_n-a)^{\top}Z_n | 1\left\{S_{n}\right\} \leq C_L  \mathbb{E}|(A_n-a)|\cdot|Z_n | 1\left\{S_{n}\right\} = C_L \epsilon M \mathbb{E}1\left\{S_{n}\right\}  \leq  C_L \epsilon M``
        - for the second term, we can use boundedness, so that ``\left|\mathbb{E} f\left(A_{n}^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z_{n}\right)\right| 1\left\{S^c_{n}\right\}\leq 2 C_{B} \mathbb{P}\left(S_{n}^{c}\right) \to 0``
    - Then the overall term converge to zero. QED.

    
## 13.2 Consistency and asymptotic normality
1. **Definition 13.2.1** A sequence of estimators ``\left\{T_{n}\right\}`` of ``\gamma=g(\theta)`` is called **consistent** if ``T_{n} \overset{\mathbb{P}_\theta}{\to} {\gamma}``   
2. **Definition 13.2.2** A sequence of estimators ``\left\{T_{n}\right\}`` of ``\gamma=g(\theta)`` is called **asymptotically normal** with *asymptotic covariance matrix* $V_\theta$ , if ``\sqrt{n}\left(T_{n}-\gamma\right) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}\left(0, V_{\theta}\right)``

## 13.3 Asymptotic linearity

- **Key Idea**: for many estimators' asymptotic normality is a consequence of asymptotic linearity, that is, the estimator is approximately *an average*, to which we can apply the CLT.
- **Definition 13.3.1** The sequence of estimators ``\left\{T_{n}\right\}`` of ``\gamma=g(\theta) \in \mathbb{R}^{p}`` is called **asymptotically linear** if there exists a function ``l_{\theta}: \mathcal{X} \rightarrow \mathbb{R}^{p}``, with ``E_{\theta} l_{\theta}(X)=0`` and ``E_{\theta} l_{\theta}(X) l_{\theta}^{T}(X)=: V_{\theta}<\infty``
    - and ``T_{n}-\gamma=\frac{1}{n} \sum_{i=1}^{n} l_{\theta}\left(X_{i}\right)+o_{\mathbb{P}_{\theta}}(1 / \sqrt{n})``
- With asymptotic linearity we have asymptotic normality ``\sqrt{n}\left(T_{n}-\gamma \right) \stackrel{\mathcal{D}}{\rightarrow} N\left(0, V_{\theta}\right)``.

### Examples

#### Example 1
``T_n = \bar{X_n}``, $\mathbb{E}T_n=\mu$, ``l_\theta(x) = x-\mu``.
#### Example 2
The second example is the unbiased variance estimator ``S^{2}:=\frac{1}{n-1} \sum_{i=1}^{n}\left(X_{i}-\bar{X}_{n}\right)^{2}``
1. we first consider the biased version ``\hat{\sigma}_{n}^{2}:=\frac{1}{n} \sum_{i=1}^{n}\left(X_{i}-\bar{X}_{n}\right)^{2}``, 
2. we can get ``S^{2}-\hat{\sigma}^{2}= S^{2}/n``, since ``S^{2}`` converge to a constant value, this estimator is also bounded in probability, so``S^{2}-\hat{\sigma}^{2}= \mathcal{O}_{\mathbb{P}}(1 / n)=o_{\mathbb{P}}(1 / \sqrt{n})``
3. ``\hat{\sigma}_{n}^{2}=\frac{1}{n} \sum_{i=1}^{n}\left(X_{i}-\mu\right)^{2}+\left(\bar{X}_{n}-\mu\right)^{2}-\frac{2}{n} \sum_{i=1}^{n}\left(X_{i}-\mu\right)\left(\bar{X}_{n}-\mu\right)=\frac{1}{n} \sum_{i=1}^{n}\left(X_{i}-\mu\right)^{2}-\left(\bar{X}_{n}-\mu\right)^{2}``
    1. based on the asymptotic normality of $\bar{X}_{n}$, the second term is ``\mathcal{O}_{\mathbb{P}_{\theta}}(1 / n)``, 
    2. Therefore ``\hat{\sigma}_{n}^{2}=\frac{1}{n} \sum_{i=1}^{n}\left(X_{i}-\mu\right)^{2}+\mathcal{O}_{\mathbb{P}_{\theta}}(1 / n) = \frac{1}{n} \sum_{i=1}^{n}\left(X_{i}-\mu\right)^{2}+\mathcal{o}_{\mathbb{P}_{\theta}}(1 / \sqrt{n})``
4. Therefore, both $S^{2}$ and $\hat{\sigma}^2_n$ both are asymptotically linear with influence function ``l_{\theta}(x)=(x-\mu)^{2}-\sigma^{2}``.
5. The asymptotic variance is ``V_{\theta}=E_{\theta}\left((X-\mu)^{2}-\sigma^{2}\right)^{2}=\kappa-\sigma^{4}``.

#### Example 3
The estimator is $\bar{X}_n^2 = (\sum_{i} x_i / n)^2$. We can simplify that ``\bar{X}_n^2  - \mu^2 = (\bar{X}_n - \mu)(\bar{X}_n + \mu) = (\bar{X}_n - \mu)^2 + 2\mu(\bar{X}_n-\mu)``

The first term is ``\mathcal{O}_{\mathbb{P}}(1/n)``. The second term is the influence function ``l_{\theta} = 2\mu(x-\mu)``. Therefore $V_\theta = 4\mu^2\theta^2$.

## Theorem 13.4.1 The ``\delta``-technique
Using Taylor expansion we arrive at this theorem
- Let ``\left(\left\{T_{n}\right\}, Z\right)`` be a collection of $\mathbb{R}^{p}$-valued random variables and ``c\in\mathbb{R}^p`` be a nonrandom vector. and ``\{r_n\}`` be a nonrandom sequence of positive numbers with ``r_{n} \downarrow 0``. Moreover let ``h: \mathbb{R}^{p} \rightarrow \mathbb{R}`` be differentiable at ``c`` with derivative ``\dot{h}(c) \in \mathbb{R}^{p}``.
    - Suppose ``\left(T_{n}-c\right) / r_{n} \stackrel{\mathcal{D}}{\longrightarrow} Z``
    - then ``\left(h\left(T_{n}\right)-h(c)\right) / r_{n} \stackrel{\mathcal{D}}{\longrightarrow} \dot{h}(c)^{T} Z``
    - and ``h\left(T_{n}\right)-h(c)=\dot{h}(c)^{T}\left(T_{n}-c\right)+o_{\mathbb{P}}\left(r_{n}\right)``.
- Proof:
    - by Slutsky's Theorem ``\dot{h}(c)^{T}\left(T_{n}-c\right) / r_{n} \stackrel{\mathcal{D}}{\longrightarrow} \dot{h}(c)^{T} Z``
    - Since ``\left(T_{n}-c\right) / r_{n}`` converges in distribution, we know that ``\left\|T_{n}-c\right\|=\mathcal{O}_{\mathbb{P}}\left(r_{n}\right)``, by Taylor expansion
        - ``h\left(T_{n}\right)-h(c)=\dot{h}(c)^{T}\left(T_{n}-c\right)+o\left(\left\|T_{n}-c\right\|\right)=\dot{h}(c)^{T}\left(T_{n}-c\right)+o_{\mathbb{P}}\left(r_{n}\right)``

### A little supplementary
In the proof, how can we get the Taylor residue ``o\left(\left\|T_{n}-c\right\|\right)`` is ``o_{\mathbb{P}}\left(r_{n}\right)``? The question becomes
- **Lemma** Given a function $o(x)$, ``\lim_{x\to 0} a(x)/x = 0``, given a random series ``B_{n} = \mathcal{O}_{\mathbb{P}}(c_n)``, where ``c_n`` is a non-random series and ``\lim_{n\to\infty} c_n = 0``,
    1. then ``B_n \overset{\mathbb{P}}{\to} 0``
    2. ``a(B_{n}) = \mathcal{o}_{\mathbb{P}}(c_n)``
- Proof:
1. to prove ``B_n \overset{\mathbb{P}}{\to} 0`` 
    1. Since ``\lim_{n\to\infty} c_n = 0``, ``\forall \epsilon,M,\exists N`` s.t. ``\forall n>N``, ``c_n<\epsilon / M``,  
    2. ``|B_n-0|>\epsilon \Leftrightarrow |\frac{B_{n}}{c_n}| > M``
    3. ``\lim_{M\to\infty}\lim_{n\to 0}P(|B_n-0|>\epsilon)  = \lim_{M\to\infty}\lim_{n\to 0}P(|\frac{B_{n}}{c_n}| > M) = 0``, ``\forall \epsilon``
    4. ``B_n \overset{\mathbb{P}}{\to} 0`` 
2. To prove ``a(B_{n}) = \mathcal{o}_{\mathbb{P}}(c_n)``, first write ``\frac{a(B_{n})}{c_n} = \frac{a(B_{n})}{B_{n}} \frac{B_{n}}{c_n}``
    1. since ``\lim_{x\to 0} a(x)/x = 0``, ``\forall \epsilon, M \exists \delta`` s.t. when ``|x|<\delta``, ``a(x)/x  < \epsilon M``
    2. Since ``B_n \overset{\mathbb{P}}{\to} 0``, ``\forall \delta`` set ``F_{n, \delta} = \{ |B_n| < \delta \}`` happens almost surely when n goes to infinity.  
    3. second term is bounded in probability by definition ``\frac{B_{n}}{c_n}=\mathcal{O}_{\mathbb{P}}(1)``, 
        1. set ``E_{n,\epsilon}=\{ |\frac{B_{n}}{c_n}| \geq  1/\epsilon\}`` have zero probability when ``\lim_{\epsilon\to 0}\lim_{n\to\infty}``
    4. By uniob bound set ``G_{n,\epsilon} = \{ |B_n| < \delta  \land |\frac{B_{n}}{c_n}| <  1/\epsilon \}`` will have almost 1 probability when ``\lim_{\epsilon\to 0}\lim_{n\to\infty}``
        1. This means ``\frac{a(B_{n})}{c_n} = \frac{a(B_{n})}{B_{n}} \frac{B_{n}}{c_n} < \epsilon  M \frac{1}{\epsilon} = M`` happens almost surely when ``\lim_{\epsilon\to 0}\lim_{n\to\infty}``, ``\forall M``.
    5. Then ``a(B_{n})/c_n \overset{\mathbb{P}}{\to} 0`` 


### Example
Consider Bernoullie distribution 
```math
    p(x)=\theta^{x}(1-\theta)^{1-x}
```
so ``\bar{X}_{n} - \theta=\frac{1}{n} \sum_{i=1}^{n}\left(x_{i}-\theta\right)``, and ``\sqrt{n} \left(\bar{x}_{n}-\theta\right) \overset{\mathcal{D}}{\to} \mathcal{N}\left(0, \theta(1-\theta)\right)``. Now we consider transformation 
```math
h(\theta) = \log\frac{\theta}{1-\theta}
```
its derivative is ``\dot{h}(\theta)=\frac{1}{\theta}+\frac{1}{1-\theta}=\frac{1}{\theta(1-\theta)}`` so 
```math
\sqrt{n}\left(\log \frac{\bar{x}_{n}}{1-\bar{x}_{n}}-\log \frac{\theta}{1-\theta}\right) \stackrel{\mathcal{D}}{\rightarrow} \mathcal{N}(0,\frac{1}{\theta(1-\theta)})
```
Now lets compare it with Cramér-Rao Lower Bound, the log of pdf is
```math
\log p_{\theta}(x)=x \log \frac{\theta}{1-\theta}+\log (1-\theta)
```
so the score function is 
```math
s_{\theta}(x)=\frac{x}{\theta(1-\theta)}-\frac{1}{1-\theta}
```
Then the fisher information is
```math
I(\theta) =\operatorname{Var}\left(s_{\theta}(x)\right)=\frac{\theta(1-\theta)}{\theta^{2}(1-\theta)^{2}} =\frac{1}{\theta(1-\theta)}
```
The estimator we consider is ``g(\theta) =  \log\frac{\theta}{1-\theta}``, one can easily varify it   fits CRLB
```math
\mathrm{CRLB} = \frac{[ \dot{g}(\theta)]^{2}}{I(\theta)}=\frac{1}{\theta(1-\theta)}
```
One can also find the variance stabilizing tranformation, which means to find $h$ such that ``(\dot{h}(\theta))^{2} / I(\theta) = (\dot{h}(\theta))^{2} \theta(1-\theta)=1``, then the solution is ``h(x)=2 \arcsin (\sqrt{x})``, so
```math
\sqrt{n}\left(2 \arcsin \left(\sqrt{\bar{x}_{n}}\right)-2 \arcsin (\sqrt{\theta})\right) \stackrel{\mathcal{D}}{\rightarrow} N(0,1)
```











