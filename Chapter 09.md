# Chapter 9 Equivariant statistics

## Exam
- Equivariance 
- Invariance 
- UMRE
    - deﬁnition
    - construction 
        - construction: iterated expectation, fubini changing order of intergration, minimization
    - Basu’s Lemma + proof 
    - examples 
        - normal distribution, uniform distribution with unknown mid point,

## Definition of location model
1. ``X_{1:n}`` i.i.d.. 
2. ``X_{i}=\theta+\epsilon_{i}``, ``\theta\in \mathbb{R}`` is the location parameter.
3. ``\epsilon`` is known with probability ``p_0(\cdot)``
4. Action space ``\mathcal{A} \subset \mathbb{R}``.

## 9.1 Equivariance and location invariant
1. **Equivariance** A *statistic* ``T=T(\mathbf{X})`` is called location *equivariant* if for all constants ``c\in\mathbb{R}`` and all ``\mathbf{x}=\left(x_{1}, \ldots, x_{n}\right)``,
    1. ``T\left(x_{1}+c, \ldots, x_{n}+c\right)=T\left(x_{1}, \ldots, x_{n}\right)+c``
2. **location invariance** A *loss function* ``L(\theta, a)`` is called *location invariant* if for all ``c \in \mathbb{R}``,
    1. ``L(\theta+c, a+c)=L(\theta, a) = L_0(a-\theta),\forall (\theta, a) \in \mathbb{R}^{2}``

### Corollary 9.1.1 
- If $T$ is equivariant and ``L(\theta, a)`` is invariant, then 
    - ``R(\theta, T)=E_{\theta} L(\theta, T(\mathbf{X}))=E_{\theta} L(0, T(\mathbf{X})-\theta) =E_{\theta} L(0, T(\mathbf{X}-\theta))=E_{\theta} L_{0}[T(\varepsilon)]``
- Because the distribution of ``\varepsilon`` does not depend on ``\theta``, we conclude that the risk does not depend on ``\theta``.
    - similarly bias variance of $T(X)$ does not depend on ``\theta``
    
### Two small lemmas
Two small lemmas are provided here for what is the set of equivariant estimator and the set of locational invariant functions as tools for later proofs. Proofs for them are simple and skipped. 
- **Lemma 1** Deﬁne the *set of invariant functions* as ``\mathcal{U}=\{u: u(X+a)=u(X), \forall a, X \in \mathcal{X}\subset \mathbb{R}^{n}\}``. 
    1. then ``\mathcal{U}=\left\{u\left(X_{1}, \ldots, X_{n}\right)=h\left(X_{1}-X_{n}, \ldots, X_{n-1}-X_{n}\right): h \text { function on } \mathbb{R}^{n-1}\right\}``   
    2. Suppose ``d(X)`` is a equivariant estimator, then ``\mathcal{U}=\left\{u\left(X_{1}, \ldots, X_{n}\right)= g\left(X_{1}-d(X), \ldots, X_{n-1}-d(X)\right): g \text { function on } \mathbb{R}^{n}\right\}``
        1. (i) is a special case of (ii)
- **Lemma 2** Let ``d(X)`` be a ﬁxed equivariant estimator. The *set of (location) equivariant estimators* is given by ``\Delta=\left\{\delta=d+u | u\in \mathcal{U}\right\}``
    - using lemma 1.i we get ``\Delta=\left\{\delta(X)=d(X) + f(X_1 - X_n,\cdots, X_{n-1} - X_n) | f \text { function defined on } \mathbb{R}^{n-1}\right\}``  
    - using lemma 1.ii we get ``\Delta=\left\{\delta(X) = d(X) + h(X-\delta(X))| h \text { function defined on } \mathbb{R}^{n}, \delta, d \text{ equivariant}\right\}``   
        - or ``\Delta=\left\{\delta(X) = d(X) + g(X-d(X))| g \text { function defined on } \mathbb{R}^{n}, d \text{ equivariant}\right\}``   

    
### Definition of Uniform Minimum Risk Equivariant
- An *equivariant* *statistic* ``T`` is called *uniform minimum risk equivariant* (**UMRE**) if ``\forall d`` equivariance decision rules(or statistics, equivalently) and ``\forall \theta`` 
    - ``R(\theta, T(X))=\min _{d \in \Delta} R(\theta, d(X)), \forall \theta``
    - or ``R(\theta, d(X)) = R(0, d(X) - \theta) = R(0, d(X - \theta)) = R(0, d(\epsilon))``, ``T = \operatorname{argmin}_{d\in \Delta} \mathbb{E}_{\epsilon}[L(0, d(\epsilon))]``

## 9.1.1 Theorem 9.1.1 & 9.1.2 Construction of the UMRE estimator
<!--- **Theorem 9.1.1** Assume 
    1. ``X=\left(X_{1}, \ldots, X_{n}\right)`` is distributed according to a location family
    2. let ``Y=\left(X_{1}-X_n, \ldots, X_{n-1}-X_n\right)`` 
    3. Assume there exists a ﬁxed equivariant estimator & 0 of ⇠ , with ﬁnite risk. If-->

    
- **Theorem 9.1.2** Assume 
    1. ``X=\left(X_{1}, \ldots, X_{n}\right)`` is distributed according to a location family ``X=\theta + \epsilon``, with ``\epsilon`` having known distribution. 
        1. (in the loss we already assume ``\theta`` is known)
    2. there exists a ﬁxed equivariant estimator ``d(X)`` with ﬁnite risk. 
    3. let ``Y=X - d(X) =:\eta(X) \in \mathbb{R}^n``, 
    4. If ``g(Y):=\arg \min _{v} \mathbb{E}_\epsilon\left[L_{0}(v+d(\epsilon)) \mid \eta(\epsilon) = Y\right]`` exists, then
        1. PS: here ``g`` is a function of ``Y``, the ``v`` above is a number in ``\mathbb{R}``
    5. ``T^{*}(X):=g(Y)+d(X) = g(\eta(X))+d(X)`` is UMRE
- Proof
    1. according to the definition of UMRE ``T^{*} = \operatorname{argmin}_{\delta \in \Delta} \mathbb{E}_{\epsilon}[L(0, \delta(\epsilon))]`` (*functional* minimization)
    2. given the third expression of ``\Delta``, we have ``\eta(\epsilon) = \epsilon - d(\epsilon)``, so that ``T^{*}(\cdot) = d(\cdot) +g(\eta(\cdot))``, 
        1. where ``g(\cdot) = \operatorname{argmin}_{g:\mathbb{R}^n \rightarrow \mathbb{R}} \mathbb{E}_{\epsilon}[L(0, d(\epsilon) + g(\eta(\epsilon)))]`` where ``\eta(\epsilon) = \epsilon - d(\epsilon)``
    3. The minimization  of ``g(\eta)`` w.r.t. the expectation is a functional, however since there is no intersection between different values of ``\eta``, they can be optimizer seperately, grouped by same value of ``\eta``.
        1. Therefore ``g(Y) = \arg\min_{v\in \mathbb{R}} \mathbb{E}_{\epsilon}[L(0, d(\epsilon) + g(Y))| \eta(\epsilon)=Y] ``. QED

**PS**
- *Depending ON ``\epsilon``'s distribution, the function ``T(X)`` have different form!!!!*
- given ``d(X) := X_n`` we arrive at theorem 9.1.1, ``T^{*}(X):=X_{n} + \arg \min _{v} E\left[L_{0}\left(v+\epsilon_{n}\right) \mid {Y}\right]``
- We don't assume i.i.d in this derivation -> Pitman estimator.

### examples of UMRE

1. For **quadratic** loss ``L_0(x) = x^2``, we have ``T^{*}(X)= d(X)-E_{\epsilon}\left[ d(x') \mid  Y(\epsilon) = Y(X) \right]``
    1. or equiavalently set ``d(X) = T^{*}(X)``, we get an equivalent condition ``E_{\epsilon}\left[T^{*}(\epsilon)  \mid  \epsilon - T^{*}(\epsilon)\right] = 0``.
2. For **L1** loss ``L_0(x) = |x|``, we have ``T^{*}(X)= d(X)-\mathrm{med}_{\epsilon}\left[ d(\epsilon) \mid  Y(\epsilon) = Y(X) \right]`` (median)

### Lemma 9.1.2 UMRE for quatradic loss Pitman estimator
We continue our calculation for the quadratic loss. ``X = \theta + \epsilon``, so that the pdf for ``X`` is ``p(\epsilon_1,\cdots,\epsilon_n)``. The pdf for ``X'`` that have same value of ``X'-X'_n = Y`` is the marginal distribution
```math
p(X' | X'-X'_n = Y) = \frac{{p}\left(y_{1}+u, \ldots, y_{n-1}+u, u\right)}{\int {p}\left(y_{1}+z, \ldots, y_{n-1}+z, z\right) d z},\text{ where }X' = Y + u + \theta,\text{ and }\epsilon = u
```
so that
```math
T^{*}(X)= d(X)-E_{x'}\left[ d(x') \mid  Y(x') = Y(X) \right] = X_n - \frac{\int u \times {p}\left(y_{1}+u, \ldots, y_{n-1}+u, u\right) du}{\int {p}\left(y_{1}+z, \ldots, y_{n-1}+z, z\right) d z}
```
By change of variable ``z \to - z + X_n``, ``u \to - z + X_n``, we have
```math
T^{*}({X})=\frac{\int z \mathbf{p}_{0}\left(X_{1}-z, \ldots, X_{n}-z\right) d z}{\int \mathbf{p}_{0}\left(X_{1}-z, \ldots, X_{n}-z\right) d z}
```

#### example 9.1.1 for Pitman estimator: uniform distribution
If ``X`` i.i.d. ``\text { Uniform }[\theta-1 / 2, \theta+1 / 2]``, then ``\mathbf{p}_{0}\left(x_{1}-z, \ldots, x_{n}-z\right)=1\left\{x_{(n)}-1 / 2 \leq z \leq x_{(1)}+1 / 2\right\}``, therefore 
```math
T^{*}=\left(\int_{T_{1}}^{T_{2}} z d z\right) /\left(\int_{T_{1}}^{T_{2}} d z\right)=\frac{T_{1}+T_{2}}{2}=\frac{X_{(1)}+X_{(n)}}{2}
```



## Maximal invariant
- A function ``f`` is called **invariant** iff ``\forall x \in\mathbb{R}^{n}, c\in\mathbb{R}, f(x) = f(x+c)``
- An *invariant* map ``\mathbf{Y}: \mathbb{R}^{n} \rightarrow \mathbb{R}^{n}`` is called **maximal invariant** if ``\mathbf{Y}(\mathbf{x})=\mathbf{Y}\left(\mathbf{x}^{\prime}\right) \Leftrightarrow \exists c \in \mathbb{R}: \mathbf{x}=\mathbf{x}^{\prime}+c, \forall x \in\mathbb{R}^{n}, c\in\mathbb{R}.``


## 9.1.4 Quadratic loss and Basu Lemma
- **Basu's Lemma** 
    1. Let ``X`` have distribution ``P_{\theta}, \theta \in \Theta``. 
    2. Suppose ``T`` is sufficient and complete 
        1. (def: if ``\mathbb{E}_{\theta}(g(T))=0`` for all ``\theta`` then ``\mathbb{P}_{\theta}(g(T)=0)=1`` for all ``\theta``), 
    3. and that ``Y = Y (X)`` has a distribution that does not depend on ``\theta``. 
    4. Then, for all ``\theta``, ``T`` and ``Y`` are independent under ``P_{\theta}``.
- Proof
    1. Denote ``g(T) = \mathbb{P}(Y\in A|T) - \mathbb{P}(Y\in A)`` 
        1. ``\mathbb{P}(Y\in A)`` does note depend on ``\theta``
        2. since ``T`` sufficient, ``P(X|T)`` does not depend on ``\theta``, so that ``\mathbb{P}(Y\in A|T)`` does not depend on ``\theta``
        3. so ``g(T)`` not depending on ``\theta``
    2. easy to check ``\mathbb{E}[g(T)] = 0``
        1. since ``T`` complete, ``\mathbb{P}[g(T) = 0 ] = \mathbb{P}[\mathbb{P}(Y\in A|T) = \mathbb{P}(Y\in A)] =  1`` 
        2. independence QED

### Example
- For normal distribution ``\mathcal{N}(\theta,\sigma^2)``, with ``\sigma^2`` known, then ``\bar{X}`` is sufficient and complete. ``\mathbf{Y}:=\mathbf{X}-\bar{X}`` does not depend on ``\theta``, so they are independent.    
- By the equivalent condition for URME in L2 loss, ``E_{\epsilon}\left[\bar{\epsilon}  \mid  \epsilon - \bar{\epsilon} \right] = E_{\epsilon}\left[\bar{\epsilon}  \right] = 0`` therefore  ``\bar{X}`` UMRE.

### Least favorable property of Gaussian distribution
For any distribution of ``\epsilon`` with zero mean and variance ``\sigma^2 = 1``, the risk of mean for locational model is all ``1/n``. For other distribution, its URME must be better than this, however it is already the best for gaussian, therefore, this is the least favorable property of Gaussian.

    
