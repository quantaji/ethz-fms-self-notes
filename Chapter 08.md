# Comparison of estimators

## Exam
Rao-Blackwell Lemma + proof
convex loss, then you can always use sufficient statistics without randomization

## 8.1 definition of risk
- **Definition** ``T(X)`` estimator, ``L(\cdot, \cdot)`` loss function 
    - risk is ``R(\theta, T):=\mathbb{E}_{\theta}(L(\theta, T(X))``

### Example
Example just want to show this framework applies to many problem
1. Hypothetis test ``H_{0}: \theta=\theta_{0}``, ``H_{1}: \theta=\theta_{1}``
    1. ``R(\theta, \phi)= \begin{cases}\mathbb{E}_{\theta_{0}} \phi(X) & \theta=\theta_{0} \\ 1-\mathbb{E}_{\theta_{1}} \phi(X) & \theta=\theta_{1}\end{cases}``
2. Estimator
    1. ``R(\theta, T):=\mathbb{E}_{\theta}(T(X)-g(\theta))^{2}=: \operatorname{MSE}_{\theta}(T)``

## 8.2 risk and sufficiency
**Key idea** Knowing the suﬃcient statistic ``S`` one can forget about the original data ``X`` without loosing information. Integration over ``X`` can be decomposed into ``S`` and ``X|S``.

### Some definition in decision theory
- Let ``\aleph`` be a set of possible actions. On ``\aleph`` we take ``\sigma``-field ``A``.
    - We say that every action induces a loss. A loss function is a function ``L: \Omega \times \aleph \rightarrow \mathbb{R}``
    - We interpret ``L(\theta, a)`` as the incurred loss if we took action ``a`` and ``\Theta=\theta``.
- A *deterministic decision* rule is a measurable function ``\delta`` from ``\mathcal{X}`` to ``\aleph``. 
    - We interpret ``\delta(X)`` as the action to take if we observe ``X``.
- A *randomized decision* is a mapping from ``\mathcal{X}`` to to a probability measure on ``(\aleph, \alpha)`` such that ``X \mapsto \delta(a ; X)`` is measurable for each ``a \in A``.
    - The loss is ``L(\theta, \delta(\cdot ; X))=\int_{\aleph} L(\theta, a) \delta(a ; X) da``

### Lemma 8.2.1
1. Suppose ``S`` is sufficient for ``\theta``. Let ``d`` be some (randomized) decision. Then there is a randomized decision ``\delta(X)`` that only depends on ``S``, such that
    1. ``R(\theta, \delta(S))=R(\theta, d), \forall \theta``

Proof
1. define the randomized decision as ``\delta(a ; X) = \delta(A ; S(X)) = E_{X'\sim p_\theta}\left[d(a ; X') \mid S(X')=S(X)\right]`` (``\delta`` here is the probability mass function)
2. The original risk can be rewritten as ``R(\theta, d) = \mathbb{E}_{x\sim p_\theta} \mathbb{E}_{a\sim d(a;X)} L(\theta, a) = \mathbb{E}_{S\sim p_\theta(S)} \mathbb{E}_{X \sim p(X|S)} \mathbb{E}_{a\sim d(a;X)} L(\theta, a)``
    1. PS: for any deterministic rule, it is also a randomized rule
3. By writing it into integration we can see that ``\mathbb{E}_{X \sim p(X|S)} \mathbb{E}_{a\sim d(a;X)} L(\theta, a) = \mathbb{E}_{a\sim \delta (a;S)} L(\theta, a)``
4. Therefore ``R(\theta, d) =  \mathbb{E}_{S\sim p_\theta(S)} \mathbb{E}_{a\sim \delta (a;S)} L(\theta, a) = R(\theta, \delta)``

## Lemma 8.3.1 Rao-Blackwell
**Key idea** Convex loss an estimator based on the original data ``X`` can be replaced by one based only on ``S`` without increasing the risk.
- Suppose 
    1. ``S`` is sufficient for ``\theta``
    2. action space ``\mathcal{A} \subset \mathbb{R}^{p}`` is convex
    3. for each ``\theta``, the map ``a \mapsto L(\theta, a)`` is convex. 
- Let ``d: \mathcal{X} \rightarrow \mathcal{A}`` be a **non-randomize** decision, and deﬁne new **non-randomized** decision rule as ``d'(s) := E(d(X) \mid S=s)`` (assumed to exist). Then ``R\left(\theta, d^{\prime}\right) \leq R(\theta, d)``

Proof
1. First since action space is convex, ``d'(s) := E(d(X) \mid S=s)`` always exists
2. ``R(\theta, d) = \mathbb{E}_{x\sim p_\theta}  L(\theta, d(X)) = \mathbb{E}_{S\sim p_\theta(S)} \mathbb{E}_{X \sim p(X|S)} L(\theta, d(X))``
    1. using Jenson's inequality ``E(g(X)) \geq g(E X)`` for convex function ``g``, apply it to term ``\mathbb{E}_{X \sim p(X|S)} L(\theta, d(X))``
    2. therefore ``\mathbb{E}_{X \sim p(X|S=s)} L(\theta, d(X)) \geq L(\theta, \mathbb{E}_{X \sim p(X|S=s)} [d(X)]) = L(\theta, d'(s))``
    3. Therefore ``R(\theta, d) = \mathbb{E}_{S\sim p_\theta(S)} \mathbb{E}_{X \sim p(X|S)} L(\theta, d(X)) \geq \mathbb{E}_{S\sim p_\theta(S)} L(\theta, d'(s) = R(\theta, d')``. QED