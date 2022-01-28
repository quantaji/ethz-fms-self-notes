# Chapter 6 Test and confidence interval

## Definition of Hypothesis Testing

- **Goal** We want to test whether given a set of data ``X``, the true paramter ``\theta`` behind is in a target set ``\Theta_0``. ``H_0:\theta\in\Theta_0``, which is called null hypothesis.
    - In this chapter, we do not emphasize on the alternative set ``H_1``, but a natural choice is ``H_1: \theta\in\Theta/\Theta_0 = \Theta_0^c``
- **We ALWAYS want to *REJECT* the null hypothesis**. The test quiterion ``\phi`` is an estimator based on observed data ``X``, ``\phi = 1`` means we *reject* the null hypothesis
    - A *non-randomized* test is when ``\phi(X)\in\{0,1\}``
    - A *randomized* test is when ``\phi(X)\in[0,1]``
        - I guess it as a interperation of rejecting with probability of ``\phi``
    - The probability of rejecting ``H_0`` with given parameter ``\theta`` is then ``E_{\theta_0} \phi(X)``
- **level** of a test, ``\alpha := \sup_{\theta\in\Theta_0}E_{\theta} \phi(X)`` is the *maximum* error of **wrong rejection** among all parameters in ``H_0``.
    - The maximum here is for consideration of worst case
    - ``E_{\theta_0} \phi(X)`` for a single ``\theta_0\in\Theta_0`` is called *type I error* or *false positive* (``H_0`` as negative)
    - Equivalently, ``\forall \theta\in\Theta_0,E_{\theta} \phi(X) \leq \alpha``
- **power** of a test, ``\inf_{\theta\in\Theta_1} E_{\theta}\phi(X)`` is the *smallest* (weakest) probability of **correct rejection** of ``H_0`` among all parameters in ``H_1``.
    - ``\beta := 1 - E_{\theta_1} \phi(X)`` for a single ``\theta_1\in\Theta_1`` is called *type II error* or *false negative*
- We define test based on ``\alpha``, e.g. we say ``\phi`` is a test at level ``\alpha``
    - the expression and threshold (e.g. reject if ``T(X) < c``) in ``\phi(X)`` is set according to ``\alpha``
        - say we find ``c`` such that ``\sup_{\theta\in\Theta_0}E_{\theta}\phi(X;c) \triangleq \alpha``, so ``c = c(\alpha)``
    - usually the null hypothesis is more computationaly approachable than the alternative hypothesis
        - the two hypothesis is not in symmetry 
- However, in practice, we can only get access to the sampled data ``X_0``
    - we want to know, *under null hypothesis*, getting this result is wether rare or common.
    - A possible approach is to choose the threshold ``c`` just as the observed value ``c = T(X_0)``, so ``\phi = 1\{T(X) > T(X_0) \}`` (for example)
        - Then we can use the level of this test ``\alpha(X_0)`` as a measure of rarity of given ``X_0``, this is the definition of **``p``-value**
        - if ``p``-value small, this means *most instance of ``H_0``* is not rejected, then ``X_0`` must be a **very rare, unlikely** case for ``H_0``
        - if ``p``-value big, say ``[0.3,1]``, this means *some common instance of ``H_0``* are also rejected, then ``X_0`` must be a **quite common case** for ``H_0``
    - In scientific research, ``H_0`` is always like "your result is bullshit, trivial, no better than random guess"
        - therefore a small ``p``-value is like, "Oh, my result is unlikely to be bullshit"
        - probably you will get a Nature for you result, so usually ``p<0.05`` is called **significant!!!**
        - I remember a teacher in high energy physics say, ``p<0.05`` is usually not enough, a deviant of ``5\sigma`` is convincing in our fields! which means ``p < 3\times 10^{-7}``.
- This leads to the formal **definition** of *``p``-value*: In null hypothesis significance testing, the ``p``-value is the probability of obtaining test results **at least as extreme as** the results actually observed, under the assumption that the *null hypothesis is correct*.

### Pivot
- In statistics, we are interested in parameter of interest ``\gamma = g(\theta)``, so our null hypothesis is like ``H_0: g(\theta) = \gamma_0``.
- **Definition** A function ``Z(X, γ )`` depending on the data ``X`` and on the parameter (of interest) ``γ`` is called a *pivot* if 
    - for all ``θ ∈ Θ``, the distribution ``\mathbb{P}_{\theta}(Z(\mathbf{X}, g(\theta)) \leq \cdot)=: G(\cdot)`` does not depend on ``θ``.
- The existance of pivot is very good thing since not depending on ``θ`` feature enable us to remove the ``\sup`` in definition of level ``\alpha`` so that obtaining confidence region and threshold is more straightforward

PS: when design test, we should not only consider rejecting region where ``p(X)`` is small, the alternative hypothesis may have similar behavor. We must catch the key difference.

## **Duality** of confidence set and *family* of hypothesis tests
- **Definition of *Confidence set***: A confidence set for parameter of intereset ``γ``, at level ``1−α``, is a mapping from given data ``X = (X_1 , . . . , X_n )`` to the space of parameter of interest ``\Gamma = g(\Theta)`` if
    - ``\mathbb{P}_{\theta}(\gamma=g(\theta) \in I) \geq 1-\alpha, \forall \theta \in \Theta``
    - or equivalently ``\alpha = \sup_{\theta\in\Theta} \mathbb{P}_{x\sim P_\theta}(\gamma = g(\theta) \notin I(X)) ``
 
### Family of Hypothesis Test => Confidence Set
1. We consider a null hypothesis of ``H_0(\gamma_0): g(\theta) = \gamma_0`` as a family of hypothesis for ``\gamma_0\in\Gamma``, ``\Theta := g^{-1}(\Gamma)``
    <!--- (Most Generally a hypothesis is of the form ``H_0: g(\theta)\in \Gamma_0``)-->
2. This family of tests ``\phi(X;\gamma_0)`` are all set to have level ``\alpha`` 
    1. so that ``\sup_{\theta;g(\theta)=\gamma_0} \mathbb{E}_{\theta}\phi(X;\gamma_0) = \alpha`` 
    2. we reject ``H_0`` if ``\phi(X;\gamma_0) = 1``. accept if ``\phi(X;\gamma_0) = 0``
3. Define the Confidence set ``I(X)`` to be ``I(X) := \{\gamma: \phi(X;\gamma) = 0\}``
    1. Then ``P_{\theta:g(\theta) = \gamma}(\gamma(\theta)\in I(X)) = P_{\theta:g(\theta) = \gamma}(\phi(X;\gamma(\theta)) = 0) = 1 - \mathbb{E}_{\theta:g(\theta) = \gamma}\phi(X;\gamma(\theta))  \geq 1 - \alpha``
    2. This is true for all ``\gamma`` for that all test have same level ``\alpha``
        1. then we can change ``P_{\theta:g(\theta) = \gamma}`` into ``P_{\theta \in \Theta}``
4. Therefore it is truely a confidence set

### Confidence Set => family of hypothesis Tests
1. We have a confidence set ``I(X)`` s.t. ``\mathbb{P}_{X\sim P_\theta}(\gamma=g(\theta) \in I(X)) \geq 1-\alpha, \forall \theta \in \Theta``
2. Define the Hypothesis family as ``H_0(\gamma_0): g(\theta) = \gamma_0``
3. and test is ``\phi(X;\gamma_0) = 1_{\{ \gamma_0 \notin I(X) \}}``
4. Then under null hypothesis ``g(\theta) = \gamma_0`` we have
    1. ``\mathbb{E}_{X\sim P_\theta}\phi(X;\gamma_0) = \mathbb{P}_{X\sim P_\theta}(\{ \gamma_0 \notin I(X) \}) = 1 - \mathbb{P}_{X\sim P_\theta}(\{ \gamma_0 \in I(X) \}) \leq \alpha``
5. Therefore each hypothesis test in this family all have level ``\alpha``



## 6.5 student test and Wilcoxon't test
**Goal**: To test whether two i.i.d. random variables ``X,Y`` have same distribution.
1. Student test
    1. under assumption of ``X,Y`` are both normal with same variance but different mean
    2. null hypothesis: the means are the same
    3. we can find a pivot: ``\sqrt{\dfrac{n m}{n+m}}\left(\dfrac{\bar{Y}-\bar{X}-\gamma}{\sigma}\right) \text { is } \mathcal{N}(0,1) \text {-distributed. }``
    4. If assume variance unknown we have to also estimate variance with ``S``
        1. a new pivot would be ``Z(\mathbf{X}, \mathbf{Y}, \gamma):=\sqrt{\dfrac{n m}{n+m}}\left(\dfrac{\bar{Y}-\bar{X}-\gamma}{S}\right)`` having Student-distribution with ``n+m−2`` degrees of freedom
2. Wixcoxon Test
    1. no further assumption of shape of distributions
    2. under null hypothesis (two distribution the same), the sum of rank ``T=T^{\text {Wilcoxon }}:=\sum_{i=1}^{n} R_{i}`` have a fixed distribution, independent of distribution
        1. ``T=\#\left\{Y_{j}<X_{i}\right\}+\frac{n(n+1)}{2}`` if ``X`` is usually bigger/smaller than ``Y``, ``T`` will deviate from null distribution
        2. under null hypothesis the set of ranks ``\{R_i\}`` is uniformly distributed with probability of ``1/N!=1/(n+m)!``
    3. This distribution is obtained by simulation for different ``(n,m)``