# Chapter 7 The Neyman Pearson Lemma and UMP tests
**In short**: find the lowest value of ``\beta`` for a fixed ``\alpha`` on ROC curve

## Definition of Uniformly Most Powerful (UMP)
- **Deﬁnition 7.0.1** A test ``φ`` is called *Uniformly Most Powerful* (UMP) at level ``\alpha`` if
    - for all tests ``\phi'`` with level ``α``, it holds that ``E_{\theta} \phi^{\prime}(X) \leq E_{\theta} \phi(X) \forall \theta \in \Theta_{1}``.
    - equivalently, same level with *highest power* or *lowest type II error*

## Neyman Pearson Lemma
NP test is for **SINGLE VALUE** hypothesis ``H_{0/1}: \theta\in\Theta_{0/1}``!!!
- **Definition** ``\phi_{\mathrm{NP}}:= \begin{cases}1 & \text { if } p_{1} / p_{0}>c \\ q & \text { if } p_{1} / p_{0}=c \\ 0 & \text { if } p_{1} / p_{0}<c\end{cases}``, ``q\in[0,1], c\in [0,+\infty)``
    - we can tune ``c`` to have level ``\alpha``

- **Lemma 7.1.1 Neyman Pearson Lemma** ``R\left(\theta_{1}, \phi_{\mathrm{NP}}\right)-R\left(\theta_{1}, \phi\right) \leq c\left[R\left(\theta_{0}, \phi\right)-R\left(\theta_{0}, \phi_{\mathrm{NP}}\right)\right]``
- straightforward, skip

## UMP extension
**Key idea**: NP test only word for single value hypothesis test, but its level and power are determined by the distribution, we can extend the parameter space by group some parameter together ``\Theta_1 = \{ \theta_1 : \mathbb{E}_{\theta_0}\phi(\theta_0, \theta_1) \leq \alpha  \} ``

- **THeorem 7.3.1** Suppose that 
    1. ``P`` is a one-dimensional exponential family ``p_{\theta}(x)=\exp [c(\theta) T(x)-d(\theta)] h(x)``, 
    2. Assume moreover that ``c(θ)`` is a strictly increasing function of ``θ``. 
    - Then a UMP test ``φ`` is ``\phi(T(x)):= \begin{cases}1 & \text { if } T(x)>t_{0} \\ q & \text { if } T(x)=t_{0} \\ 0 & \text { if } T(x)<t_{0}\end{cases}``
        - where ``t_0`` is chosen to have ``E_{\theta_{0}} \phi(T)=\alpha``.
- *Proof*
    1. First for each ``\theta_0`` and ``\theta_1``, 
        1. since ``\frac{p_{\theta_{1}}(x)}{p_{\theta_{0}}(x)}=\exp \left[\left(c\left(\theta_{1}\right)-c\left(\theta_{0}\right)\right) T(x)-\left(d\left(\theta_{1}\right)-d\left(\theta_{0}\right)\right)\right]``
        2. and ``\frac{p_{\theta_{1}}(x)}{p_{\theta_{0}}(x)} \lesseqgtr c \Leftrightarrow T(x) \lesseqgtr t`` 
        3. the test is NP so it is UMP
    2. Now we have to verify set ``H_0: \theta \leq \theta_0`` have level smaller than ``\alpha``, ``\alpha \geq \mathbb{E}_{\theta}\phi(T)``
        1. This is done by proving ``\mathbb{E}_{\theta}\phi(T)`` is increasing
        2. ``\begin{aligned}
\beta(\vartheta)-\beta(\theta) &=\int \phi(t)\left[\bar{p}_{\vartheta}(t)-\bar{p}_{\theta}(t)\right] d \bar{\nu}(t) \\
&=\int_{t \leq s_{0}} \phi(t)\left[\bar{p}_{\vartheta}(t)-\bar{p}_{\theta}(t)\right] d \bar{\nu}(t)+\int_{t \geq s_{0}} \phi(t)\left[\bar{p}_{\vartheta}(t)-\bar{p}_{\theta}(t)\right] d \bar{\nu}(t) \\
& \geq \phi\left(s_{0}\right) \int\left[\bar{p}_{\vartheta}(t)-\bar{p}_{\theta}(t)\right] d \bar{\nu}(t)=0 .
\end{aligned}``
            1. The threshold is choosed based on ``\begin{cases}\frac{\bar{p}_{\vartheta}(t)}{\bar{p}_{\theta}(t)} \leq 1 & \text { for } t \leq s_{0} \\ \bar{p}_{\vartheta}(t) & \text { for } t \geq s_{0}\end{cases}``
            2. Both ``\phi(\cdot)`` and ``\left[\bar{p}_{\vartheta}(t)-\bar{p}_{\theta}(t)\right]`` is increasing w.r.t ``t`` this gives the inequality

    
## 7.5 Unbiased tests
- **Deﬁnition 7.5.1** A test ``φ`` is called unbiased if for all ``θ ∈ Θ_0`` and all ``ϑ ∈ Θ_1``, 
    - ``E_{\theta} \phi(X) \leq E_{\vartheta} \phi(X)``
- ``\alpha + \beta \leq 1``

I don't know how to understand this theorem but I write it here any way

- **Theorem 7.5.1 (no proof)** Suppose 
    1. ``\mathcal{P}`` is a one-dimensional exponential family ``\frac{d P_{\theta}}{d \nu}(x):=p_{\theta}(x)=\exp [c(\theta) T(x)-d(\theta)] h(x)``
    2. ``c(θ)`` strictly increasing in ``θ``.
    - Then a UMPU test is ``\phi(T(x)):= \begin{cases}1 & \text { if } T(x)<t_{L} \text { or } T(x)>t_{R} \\ q_{L} & \text { if } T(x)=t_{L} \\ q_{R} & \text { if } T(x)=t_{R} \\ 0 & \text { if } t_{L}<T(x)<t_{R}\end{cases}``
        - where the constants ``t_R , t_L , q_R`` and ``q_L`` are chosen in such a way that 
        - ``E_{\theta_{0}} \phi(X)=\alpha,\left.\frac{d}{d \theta} E_{\theta} \phi(X)\right|_{\theta=\theta_{0}}=0``