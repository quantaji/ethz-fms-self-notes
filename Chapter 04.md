# Chapter 4 Sufficiency and exponential families
just a small notes on minimal sufficiency
- **Definition** A sufficient statistic ``T`` is *minimal* if 
    - for every sufficient statistic ``T'`` and for every ``x, y ∈ \mathcal{X}``, ``T(x) = T(y)`` whenever ``T'(x) = T'(y)``. 
    - In other words, ``T`` is a function of ``T'``,
    - or there exists ``f`` such that ``T(x) = f(T'(x))``for any ``x ∈ X``.

This defination deviates from that provided in the textbook. The following Theorem shows the connection.

- **Theorem** Let ``\{ p(x| θ), θ ∈ Ω \}`` be a family of densities with respect to some measure ``µ``. Suppose that there exists a statistic ``T`` such that for every ``x, y ∈ \mathcal{X}``, ``p(x ; \theta)=C_{x, y} p(y ; \theta)  \Leftrightarrow  T(x)=T(y)`` for every ``θ`` and some ``C _{x,y}∈ \mathbb{R}``. Then ``T`` is 
    1. sufficient, 
    2. minimal sufficient.
- **Proof**  
    1. Denote ``T(\mathcal{X})=\{t: t=T(x) \text { for some } x \in \mathcal{X}\}`` as the range of statistic ``T``.
    2. For each ``t ∈ T(\mathcal{X})``, consider the preimage ``A_t = T^{-1}(t) = \{x| T(x) = t \}`` and select an arbitrary representative ``x_t`` from each ``A_t``. Then, for any ``y \in \mathcal{X}`` we have 
        1. ``y \in A_{T(y)}``
        2. ``x_{T(y)} \in A_{T(y)}``.
    3. Therefore for any ``y``, ``T(y)=T\left(x_{T(y)}\right)``
    4. By the assumption of the theorem ``p(y ; \theta)=C_{y, x_{T(y)}} p\left(x_{T(y)} ; \theta\right)=h(y) g_{\theta}(T(y))``
        1. Therefore by the factorization theorem $T$ is *sufficient*
    5. Consider another sufficient statistic ``T'``, also by factorization theorem we have ``p(x ; \theta)=\tilde{g_{\theta}}\left(T^{\prime}(x)\right) \tilde{h}(x)``
        1. ``\forall (x,y)`` s.t. ``T^{\prime}(x)=T^{\prime}(y)`` we have ``p(x ; \theta)=\tilde{g}_{\theta}\left(T^{\prime}(x)\right) \tilde{h}(x)=\tilde{g}_{\theta}\left(T^{\prime}(y)\right) \tilde{h}(y) \frac{\tilde{h}(x)}{\tilde{h}(y)}=p(y ; \theta) C_{x, y}``
        2. By the assumption of this theorem we also have ``T(x)=T(y)``
        3. So, ``T^{\prime}(x)=T^{\prime}(y)`` implies ``T(x) = T(y)`` for any sufficient statistic ``T'`` and any ``x, y``. Therefore, ``T`` is a *minimal*.