# Chapter 11 Proving admissibility and minimaxity

## Exam
- Extended Bayes 
- Lemma 11.1.1 + proof  
    - examples 
- Lemma 11.2.1 + proof 
- Lemma 11.2.2 + proof
- ``X\sim \mathcal{N}(\mu,1)``
    - (in)admissible estimators of ``\mu`` + proof

### Extended Bayes
- **Definition 11.0.1** A statistic ``T`` is called *extended Bayes* if 
    - there exists a sequence of prior densities ``\left\{w_{m}\right\}_{m=1}^{\infty}`` (w.r.t. dominating measures that are allowed to depend on ``m``), such that ``r_{w_{m}}(T)-\inf _{T^{\prime}} r_{w_{m}}\left(T^{\prime}\right) \rightarrow 0`` as ``m → ∞``.
    - In this sence ``T`` is approaching optimal compared with the true optimal estimator for each ``m``.

## 11.1 Minimaxity
- **Lemma 11.1.1** Suppose ``T`` is a statistic with risk ``R(θ, T) = R(T)`` not depending on ``θ``. Then any of the following condition leads to minimaxity:
    1. *admissible* 
    2. *Bayes*
    3. *extended Bayes*
- *Proof*
    1. admissible -> ``\forall T'``, either
        1. ``\exists \theta`` s.t. ``R(\theta, T) < R(\theta, T') \leq  \sup_{\theta}R(\theta, T')``
            1. since ``R(\theta, T)`` not depending on ``\theta``, ``\sup_{\theta} = |_\theta``
            2. ``\forall \theta``, ``\sup_{\theta} R(\theta, T)\leq \sup_{\theta}R(\theta, T')``
        2. ``\forall \theta``, ``R(\theta, T) \leq R(\theta, T')`` -> ``\sup_{\theta}R(\theta, T) = R(T) \leq \sup_{\theta}R(\theta, T')``
    2. Bayes w.r.t ``w``
        1. since not depending on ``\theta``, ``r_w(T) = R(T)``
        2. ``\sup_{\theta}R(\theta, T) = R(T) = r_w(T) \leq r_w(T') \leq \sup_{\theta}R(\theta, T')``
    3. Extended Bayes, w.r.t ``w_m``
        1. since not depending on ``\theta``, ``r_w(T) = R(T)``
        2. ``\sup_{\theta}R(\theta, T) = R(T) = r_w(T) \leq \epsilon + \inf_{T'} r_w(T') \leq \epsilon + \inf_{T'}\sup_{\theta}R(\theta, T'), \forall \epsilon``


This theorem seems very limited, ``R(θ, T) = R(T)`` not depending on ``θ`` happens very rare. (?)     

### Examples for Binomial
A very very special case, where using a Beta distribution of specifically choosen parameter can lead to the loss not depending on parameter, which lead to minimax.

### 11.1.1 minimaxity for Pitman estimator (for quadratic loss)

Interesting, but skipped, because teacher skip this. See notes. Use a enlarging uniform distribution as series.

## 11.2 Bayes -(under some condition)-> Admissibility
In this section assume
1. parameter space ``\Theta`` is assumed to be an open subset of a topological space, so that we can consider open neighborhoods of members of ``Θ``, and continuous functions on ``Θ``.
2. statistics ``T`` with ``R(θ, T) < ∞``

- **Definition** The statistic ``T`` is called *unique Bayes* decision if 
    - ``r_w(T) = r_w(T′) `` implies that ``∀ θ, T = T'\text{ }P_θ``-almost surely), 
- **Lemma 11.2.1** Suppose that the statistic ``T`` is *Bayes* for the prior density ``w``. Then either condition below are sufficient conditions for the **admissibility** of *T*.
    1. The statistic *T* is the *unique Bayes* decision.
    2. For all ``T'``, ``R(θ, T')`` is continuous in ``θ``
        1. and moreover, for all open ``U ⊂ Θ``, the prior probability ``Π(U) := ∫ U w(ϑ)d µ (ϑ)`` of ``U`` is strictly positive.
- *Proof*
    - If not admissible, ``\exists T'`` such that ``\forall \theta``. ``R(\theta, T) \geq R(\theta, T')`` and ``\exists \theta_0`` such that ``R(\theta_0, T) > R(\theta_0, T')``
        - so that ``r_w(T') \leq r_w(T)``
    - But ``T`` Bayes, ``\forall T'``, ``r_w(T') \geq r_w(T)``
        - therefore  ``r_w(T') = r_w(T)``
    1. Case (i) unique Bayes impies ``T = T'`` almost surely for all ``\theta`` -> ``R(\theta, T)  = R(\theta, T')`` for all ``\theta`` -> **contradictory**!
    2. Case (ii) use an open set near ``\theta_0`` to prove that ``r_w(T') - r_w(T) = \int R(\theta, T') - R(\theta, T) d\Pi_\theta`` is strictly positive -> **contradictory**!
        1. include use of continuity of ``R(\theta,T)`` w.r.t ``\theta``.

- **Lemma 11.2.2** Suppose that 
    1. ``T`` is extended Bayes, 
    2. for all ``T'``, ``R(θ, T')`` is continuous in ``θ``
    3. for all open sets ``U ⊂ Θ``,
        1. ``\dfrac{r_{w_{m}}(T)-\inf _{T^{\prime}} r_{w_{m}}\left(T^{\prime}\right)}{\Pi_{m}(U)} \rightarrow 0`` as ``m\to\infty``
            1. Here ``\Pi_{m}(U):=\int_{U} w_{m}(\vartheta) d \mu_{m}(\vartheta)`` is the probability of ``U`` under the prior ``Π_m``.
            2. which means probability mass distribute "equally" in parameter space wrt the risk.
- *Proof*
    - If not admissible, ``\exists T'`` such that ``\forall \theta``, ``R(\theta, T) \geq R(\theta, T')`` and ``\exists \theta_0`` such that ``R(\theta_0, T) > R(\theta_0, T')`` 
        - By condition (ii) ``\exists \epsilon >0`` and an open set ``U`` where ``\theta_0\in U`` such that  ``R(\theta_0, T) - R(\theta_0, T') > \epsilon`` 
        - integration in this open set leads to ``\int_U R(\theta, T') - R(\theta, T) d\Pi_\theta >  \epsilon \Pi_{w_m}(U)``, for all ``m``
        - By the condition of ``\forall \theta``, ``R(\theta, T) \geq R(\theta, T')``, we have ``r_{w_m}(T) - r_{w_m}(T') \geq \epsilon \Pi_{w_m}(U)`` for all ``m``
            - or equivalently ``\dfrac{r_{w_m}(T) - r_{w_m}(T')}{\Pi_{m}(U)}> \epsilon`` for all ``m``
    - By condition (iii), and the fact that ``r_{w_m}(T) - r_{w_m}(T') \leq r_{w_{m}}(T)-\inf _{T^{*}} r_{w_{m}}\left(T^{*}\right)``
        - so that ``\dfrac{r_{w_m}(T) - r_{w_m}(T')}{\Pi_{m}(U)} \leq 0`` for all ``m`` -> **Contradictory**
   
**PS**: where we use extended Bayes condition??? If the prior ``w_m`` is suitable we can truely get extended Bayes.


### Admissible estimator for normal mean ``X\sim \mathcal{N}(\theta, 1)`` under quadratic loss (important)
- Let ``X`` be ``\mathcal{N}(\theta, 1)``-distributed, ``\theta \in \Theta:=\mathbb{R}`` and ``R(\theta, T):=E_{\theta}(T-\theta)^{2}`` be the quadratic risk. We consider estimators of the form ``T=a X+b, a>0, b \in \mathbb{R}``
- **Lemma** ``T`` is admissible if and only if one of the following cases hold
    1. ``a<1``
    2. ``a=1 \text { and } b=0`` 
- *Proof*
    1. If both condition not hold, we have ``a > 1``, based on bias variance decomposition we have
        1. ``R(\theta, aX+b) = \text{Var}[aX+b] + (a\mathbb{E}X+b-\theta)^2 = a^2 + [(a-1)\theta+b]^2 \leq a^2 > 1``
        2. This risk is larger than ``a=1, b=0`` case, so inadmissible.
    2. The risk formula ``R(\theta, aX+b) = a^2 + [(a-1)\theta+b]^2 \leq a^2`` shows continuity in ``\theta``
    3. Case (i) ``a<1``, **idea** is that we construct a Bayes estimator, that is exactly ``aX+b``
        1. consider a Gaussian prior on ``\theta \sim \mathcal{N}(c, \tau^2)``
            1. conditional distribution ``P(\theta, X) \propto \exp(- \dfrac{1}{2}(  (\theta-c)^2/\tau^2 + (x-\theta)^2  )) \propto \exp(- \dfrac{1}{2}( \theta^2(1+1/\tau^2) - 2\theta(x+c/\tau^2)  ))``
            2. posterior distribution is ``\mathcal{N}(\dfrac{x \tau^2 + c}{\tau^2+1}, \dfrac{\tau^2}{\tau^2+1})``
        2. Then the Bayes estimator for quatratic loss is ``T = \mathbb{E}[ \theta | X ] = \dfrac{x \tau^2 + c}{\tau^2+1}``
            1. by setting ``a = \dfrac{\tau^2}{\tau^2+1} < 1`` and ``b = \dfrac{c}{\tau^2+1}`` (which solution always exists)
        3. Since a gaussian prior have positive distribution density, all open set have strictly positive probability mass, by lemma 11.2.1 (ii) -> ``T`` is admissible
    4. Case (ii) **Key idea** The problem here is that a gaussian prior cannot have ``a = 1``, but we can use extended Bayes to do it asymptotically
        1. let the series of prior be ``\theta\sim \mathcal{N}(0,m)``
            1. The Bayes estimator is then ``T_m(X) = \frac{m}{m + 1} X``, and its risk is ``R(\theta, T_m) = a^2 + (1-a)^2\theta^2 = \dfrac{m^2 + \theta^2}{(m + 1)^2}``
            2. The Bayesian risk is then ``r_m(T_m) = \dfrac{m^2 + \mathbb{E} \theta^2}{(m + 1)^2} = \dfrac{m}{(m + 1)}``
            3. ``\lim_{m\to\infty}r_m(T_m) = 1``,
        2. The Bayesian risk for ``X``  is then ``r_m(T) = \mathbb{E}_{\theta}R(\theta, X) = \mathbb{E} 1 = 1``
            1. therefore ``X`` is extended Bayes
        3. For any open set  ``(a,b)\in \mathbb{R}``, we have ``\Pi_{(a,b)} \geq |b-a|\cdot\exp(-\max\{|b|, |a|\}^2/m)/\sqrt{m}``
            1. Therefore ``\dfrac{r_m(T) - r_m(T_m)}{\Pi_{(a,b)}} \leq \frac{1}{m |b-a|\cdot\exp(-\max\{|b|, |a|\}^2/m)/\sqrt{m}} = O(\exp(A/m)/\sqrt{m}) \to 0``
        4. By lemma 11.2.2 we have ``T=X`` is admissible.
         

