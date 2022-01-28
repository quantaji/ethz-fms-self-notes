# Chapter 14 M-estimator

## Exam
- M-estimator 
    - deﬁnition 
    - examples
- Lemma 14.1.1 + proof 
- Thm 14.2.1 + proof 
- Thm 14.2.2 + proof 
- Inﬂuence function 
    - M-estimator (without proof) 
- Asymp. rel. eﬃciency 
    - deﬁnition 
    - examples
- Lemma 14.8.1 (no proof)
    - examples
- Lemma 14.10.1 (no proof)
    - examples

## some definitions
1. assume loss ``L(\theta, d(x))`` only depends on parameter of interest, ``\gamma = g(\theta)``
    1. loss rewrite as ``L(\theta, d(x)) =: \rho_\gamma(x)``
2. *theoretical risk* ``\mathcal{R}(c) := \mathbb{E}_\theta[\rho_c(X)] = \int \rho_c(X) dF_\theta(X)``
    1. the index $\theta$ means the distribution is a function of parameter $\theta$
    2. We require that ``\mathcal{R}(c)`` is minimized at ``\gamma=\arg \min _{c \in \Gamma} \mathbb{E}_\theta[\rho_c(X)]=\arg \min _{c \in \Gamma} \mathcal{R}(c)``
    3. PS: we can alternatively define $\gamma = g(\theta)$ in this way.
3. *empirical risk* ``\hat{\mathcal{R}}_{n}(c):=\frac{1}{n} \sum_{i=1}^{n} \rho_{c}\left(X_{i}\right), c \in \Gamma .``
    1. ***M-estimator***: ``\hat{\gamma}_{n}:=\arg \min _{c \in \Gamma} \frac{1}{n} \sum_{i=1}^{n} \rho_{c}\left(X_{i}\right)=\arg \min _{c \in \Gamma} \hat{\mathcal{R}}_{n}(c)``
        1. M-estimator is not explicit, compared with previous estimators (I think this is the main difficulty).
        2. The main focus in this chapter is, how we quantify the difference b.t.w. ``\hat{\gamma}_{n}`` and ``\gamma``.
4. if ``\forall x``, ``\rho_c(x)`` is differentiable w.r.t. $c$, define ``\psi_c(x) := \dot{\rho}_{c}(x):=\frac{\partial}{\partial c} \rho_{c}(x)``
    1. we assume the differentiation and expectation can be interchange all the time.
    2. so similarly ``\dot{\mathcal{R}}(c) := \mathbb{E}_\theta[\dot{\rho}_c(X)] = \int \dot{\rho}_c(X) dF_\theta(X)``
        1. and ``\dot{\mathcal{R}}(\gamma) = 0``
    3. ``\dot{\hat{\mathcal{R}}}_{n}(c)=\frac{\partial}{\partial c} \frac{1}{n} \sum_{i=1}^{n} \rho_{c}\left(X_{i}\right)=\frac{1}{n} \sum_{i=1}^{n} \psi_{c}\left(X_{i}\right)``
    4. ***Z-estimator*** is defined as the solution of ``\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right)=0``

**Ideas**: M-estimators are not explicit, this makes the use of law of large number does not lead directly from empirical risk to theoretical risk. Therefore, we need additional effort to prove them with the tools of empirical process.    

## 14.1 MLE as a special case of M-estimator
1. denote ``\theta`` as the true parameter for distribution ``p_\theta``, and ``\tilde{\theta}`` as the assume parameter.
    1. the Maximum (Log) Likelihood estimator is defined as finding ``\tilde{\theta}`` that gives maximum log-likelihood. 
    2. The loss is ``\rho_{\tilde{\theta}} = - \log p_{\tilde{\theta}}(x)``
    3. The empirical risk is ``\hat{\mathcal{R}}_{n}(\tilde{\theta}) = - \sum_{i} \log p_{\tilde{\theta}}(X_i)``.
    4. The theoretical risk is ``\mathcal{R}_{n}(\tilde{\theta}) = - \mathbb{E}_{\theta} \log p_{\tilde{\theta}}(X_i)``.
2. *Kullback Leibler divergence* or *Kullback Leibler information* or *relative entropy*
    1. ``K(\tilde{\theta} \mid \theta)=E_{\theta} \log \left(\frac{p_{\theta}(X)}{p_{\tilde{\theta}}(X)}\right)``
    2. using Jensen's inequality, ``\mathbb{E} \log \leq \log \mathbb{E}``, we have ``K(\tilde{\theta} \mid \theta) \geq 0``
        1. equality holds when ``p_\theta = p_{\tilde{\theta}}``

### Lemma 14.1.1
1. The theoretical MLE risk can be seen as 
    1. ``K(\tilde{\theta} \mid \theta)=\mathcal{R}(\tilde{\theta})-\mathcal{R}(\theta)``
    2. which means The function ``\mathcal{R}(\tilde{\theta})=-E_{\theta} \log p_{\tilde{\theta}}(X)`` is minimized at ``\tilde{\theta}=\theta``, ``\theta=\arg \min _{\tilde{\theta}} \mathcal{R}(\tilde{\theta})``.

## 14.2 Consistency of M-setimators  and Z-estimator

**Key idea of this section**

For M-estimators: **Compactness over paramter space** -[*Lemma 14.2.1*]-> **uniform convergence** -[*Theorem 14.2.1*]-> **Consistency of risk** -[*Assumption for well seperateness*]-> **Consistency of M-estimator** ✅

For Z-estimator (differentiable case): *Theorem 14.2.2*

### Notation
1.$f(X)$ any function, $\theta$ parameter for the true distribution
    1. ``P_\ f := \mathbb{E}_{X\sim p_\theta}[f(X)]``, denoting theoretical expectation
    2. ``\hat{P}_{n} f:=\frac{1}{n} \sum_{i=1}^{n} f\left(X_{i}\right)``, where ``X_i\sim p_\theta``, denoting the emperical observation
        1. the second definition is stochastic, by its sampling nature.
2. the empirical/theoretical risk is then ``\hat{\mathcal{R}}_{n}(c)=\hat{P}_{n} \rho_{c}, \mathcal{R}(c)=P_{\theta} \rho_{c}``

### Strong Law of Large numbers (LLN) in this problem (no proof)
- For funciton ``f(x)``, if ``P_{\theta}|f|<\infty``, then ``\left|\left(\hat{P}_{n}-P_{\theta}\right) f\right| \rightarrow 0, \mathbb{P}_{\theta}-\text{a.s.}``

### Lemma 14.2.1  **Compactness over paramter space** --> **uniform convergence**
- Suppose
    1. parameter space ``\Gamma`` is compact, 
    2. ``\forall x``, mapping ``c \mapsto \rho_{c}(x)`` is continuous
    3. ``P_{\theta}\left(\sup _{c \in \Gamma}\left|\rho_{c}\right|\right)<\infty`` (*for the use of LLN*)
- Then we have uniform convergence ``\sup _{c \in \Gamma}\left|\left(\hat{P}_{n}-P_{\theta}\right) \rho_{c}\right| \rightarrow 0, \mathbb{P}_{\theta}-\text {a.s.}``

#### Proof
1. for each ``\delta > 0`` and ``c \in \Gamma``, define ``w(x,\delta,c) := \sup _{\tilde{c} \in \Gamma:\|\tilde{c}-c\|<\delta}\left|\rho_{\tilde{c}}(x)-\rho_{c}(x)\right|``
    1. by assumption (ii) we have ``\lim_{\delta \downarrow 0} w(x, \delta, c) \rightarrow 0``
    2. similarly the average ``\lim_{\delta \downarrow 0} P_{\theta} w(\cdot, \delta, c) \rightarrow 0``
    3. ``\forall \epsilon``, define ``\delta_c`` such that ``P_{\theta} w\left(\cdot, \delta_{c}, c\right) \leq \epsilon``.
2. Define ``B_{c}:=\left\{\tilde{c} \in \Gamma:\|\tilde{c}-c\|<\delta_{c}\right\}``,
    1. Then ``\left\{B_{c}: c \in \Gamma\right\}`` is a covering set of ``\Gamma``.
    2. By assumption (i), there exists finite sub-covering ``B_{c_{1}} \ldots B_{c_{N}}``.
    3. In each $c \in B_{c_{j}}$, we have ``\left|\rho_{c}(x)-\rho_{c_{j}}(x)\right| \leq w\left(x, \delta_{c_{j}}, c_{j}\right)`` (definition of ``w``)
3. ``\left(\hat{P}_{n}-P_{\theta}\right) \rho_{c} = \left(\hat{P}_{n}-P_{\theta}\right) \rho_{c_j} + \hat{P}_{n}( \rho_{c} -  \rho_{c_j}) -P_{\theta}( \rho_{c} -  \rho_{c_j}) ``
    1. By triangular inequation ``\left|\left(\hat{P}_{n}-P_{\theta}\right) \rho_{c}\right| \leq |\left(\hat{P}_{n}-P_{\theta}\right) \rho_{c_j}| + |\hat{P}_{n}( \rho_{c} -  \rho_{c_j}) |  + |P_{\theta}( \rho_{c} -  \rho_{c_j})|``
    2. Then ``\sup _{c \in \Gamma} \left|\left(\hat{P}_{n}-P_{\theta}\right) \rho_{c}\right| \leq \max _{j\in[N]}|\left(\hat{P}_{n}-P_{\theta}\right) \rho_{c_j}| + \max _{j\in[N]}|\hat{P}_{n}( \rho_{c} -  \rho_{c_j}) |  + \max _{j\in[N]}|P_{\theta}( \rho_{c} -  \rho_{c_j})|``
        1. The first term converge to $0$ almost surely by **LLN**
        2. The third term is no bigger than ``\epsilon`` by the definition of $\delta_c$ (1.iii)
        3. The second term converge to the third term by **LLN** almost surely
    3. In all ``\sup _{c \in \Gamma} \left|\left(\hat{P}_{n}-P_{\theta}\right) \rho_{c}\right| \leq 2\epsilon`` almost surely, ``\forall \epsilon``. QED

### Theorem 14.2.1 **uniform convergence** --> **Consistency of risk**
1. Suppose the uniform convergence ``\sup _{c \in \Gamma}\left|\hat{\mathcal{R}}_{n}(c)-\mathcal{R}(c)\right| \rightarrow 0, \mathbb{P}_{\theta}-\text {a.s.}``
    1. then we have consistency for the risk ``\mathcal{R}\left(\hat{\gamma}_{n}\right) \rightarrow \mathcal{R}(\gamma), \mathbb{P}_{\theta}-\text {a.s.}``.

#### Proof
- Key idea is using triangular inequation with the help of ``\hat{\mathcal{R}}_{n}(\gamma)`` and ``\hat{\mathcal{R}}_{n}(\hat{\gamma}_n)`` as anchors.
    1. Since ``\mathcal{R}(\gamma)`` is the minimum, ``\mathcal{R}\left(\hat{\gamma}_{n}\right) - \mathcal{R}(\gamma) > 0`` and is roughly decreasing over $n$.
    2. ``\mathcal{R}\left(\hat{\gamma}_{n}\right) - \mathcal{R}(\gamma) = \left( \mathcal{R}\left(\hat{\gamma}_{n}\right) - \hat{\mathcal{R}}_{n}(\hat{\gamma}_n) \right) +  \left( \hat{\mathcal{R}}_{n}(\hat{\gamma}_n) - \hat{\mathcal{R}}_{n}(\gamma) \right) + \left( \hat{\mathcal{R}}_{n}(\gamma) - \mathcal{R}(\gamma) \right)``
    3. The first and third term converge to zero almost surely, by the assumption of uniform convergence
    4. The second term is negative and converge to non-positive, because ``\hat{\mathcal{R}}_{n}(\hat{\gamma}_n)`` is minimum over all ``\hat{\mathcal{R}}_{n}(c)``
    5. Then the sum of three term is then non-positive, togethor with (i), we can prove it converge to zero. QED

### Well seperateness **Consistency of risk** --> **Consistency of M-estimator**
- Definition: The minimizer ``\gamma`` of ``\mathcal{R}(c)`` is called well-separated if ``\forall \epsilon > 0``, ``\inf \{\mathcal{R}(c): c \in \Gamma,\|c-\gamma\|>\epsilon\}>\mathcal{R}(\gamma)``
- If ``\gamma`` is well-separated, consistency over risk ``\mathcal{R}\left(\hat{\gamma}_{n}\right) \rightarrow \mathcal{R}(\gamma)``, ``\mathbb{P}_{\theta^{-}} \text{a.s.}`` implies consistency of M-estimator ``\hat{\gamma}_{n} \rightarrow \gamma ``, ``\mathbb{P}_{\theta^{-}} \text{a.s.}``.

### Theorem 14.2.2 Consistency for Z-estimator: **``C^1``-continuity for ``\rho``** --> consistency
1. Suppose
    1. ``\Gamma \subset \mathbb{R}`` 
    2. ``\psi_{c}(x)`` is continuous in $c$ for all $x$
    3. ``P_{\theta}\left|\psi_{c}\right|<\infty, \forall c`` (*for the use of LLN*)
    4. ``\exists \delta > 0`` s.t.
        1. ``\forall c, \gamma<c<\gamma+\delta, \dot{\mathcal{R}}(c)>0``
        2. ``\forall c, \gamma-\delta<c<\gamma, \dot{\mathcal{R}}(c)<0``
2. Then 
    1. ``\mathbb{P}\left(\exists \hat{\gamma}_{n}: \dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right)=0\right) \rightarrow 1``, the Z-estimator exists almost surely. 
    2. ``\left\|\hat{\gamma}_{n}-\gamma\right\|=\mathcal{o}_{\mathbb{P}}(1)``, the solution is consistent

#### Proof
**The key idea** is to use *intermediate value theorem* for ``\dot{\hat{\mathcal{R}}}_{n}(c)``, the positive/negative sign can be ensured by that of ``\dot{\mathcal{R}}_{n}(c)`` and **LLN**.
1. for arbitary ``\epsilon`` s.t. ``0<\epsilon<\delta``, by assumption (iv) ``\exists \tilde{\epsilon}`` s.t. ``\dot{\mathcal{R}}(\gamma+\varepsilon) \geqslant 2 \tilde{\varepsilon}``, and ``\dot{\mathcal{R}}(\gamma-\varepsilon) \leqslant-2 \tilde{\varepsilon}``.
2. Now we want to prove that for ``\dot{\hat{\mathcal{R}}}_{n}(\hat{\gamma}_n \pm \epsilon)`` have different sign when ``n`` is large enough,
    1. denote set ``A=\left\{\dot{\hat{\mathcal{R}}}_{n}(\gamma+\varepsilon)-\dot{\mathcal{R}}(p+\varepsilon)>-\tilde{\varepsilon} \text { and } \dot{\hat{\mathcal{R}}}_{n}(\gamma-\varepsilon)-\dot{\mathcal{R}}(\gamma-\varepsilon)<\tilde{\varepsilon}\right\}`` 
    2. by **LLN**, ``\mathbb{P}\left(A^{c}\right) \rightarrow 0``, so set ``A`` happens almost surely,
    3. under condition of set ``A``, we have ``\dot{\hat{R}}_{n}(\gamma+\epsilon) \geq \tilde{\epsilon}`` and ``\dot{\hat{R}}_{n}(\gamma+\epsilon) \leq - \tilde{\epsilon}``
3. By *intermediate value theorem*, under condition of  set ``A`` (which happens almost surely), solutions ``\exists \hat{\gamma}_{n}: \dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right)=0`` exists.
4. Since ``\epsilon`` arbitary, ``\left\|\hat{\gamma}_{n}-\gamma\right\|=\mathcal{o}_{\mathbb{P}}(1)``, the solution is consistent.

## 14.3 Asymptotic normality of M(Z)-estimator
**Key idea**: 
1. The asymptotic normality is obvious for asymptotic linear expression, 
    1. which means ``\sqrt{n}\left(\hat{P}_{n}-P_{\theta}\right) f \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}(0, \Sigma)`` by **CLT**. 
2. However since M-estimator is implicit, it may not be written in the form of ``\hat{P}_{n} f``. 
    1. We need to use the condition of 
        1. ``\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right)=0, \dot{\mathcal{R}}(\gamma)=0`` 
        2. and the asymptotic linearity of ``\dot{\hat{\mathcal{R}}}_{n}\left( c \right)`` 
    2. to get the **asymptotic linearity for ``\hat{\gamma}_{n}``**
3. A similar problem is this example: 
    1. ``x_0(\theta)`` is the root of ``f(x;\theta)``, 
    2. ``g(x) = f_0(x) + \theta f_1(x)`` is the first order approximation for ``f(x;\theta)``.
    3. the root ``x_{1}(\theta)`` of ``g(x) = 0`` then is also the first order approximation for ``x_0(\theta)``.
    4. The proof involves derivative of inverse function
4. Theorem 14.3.1 is just a stochastic version of this problem.

### Definition of asymptotical continous

1. *empirical process*: The stochastic process ``\left\{\nu_{n}(c): c \in \Gamma\right\}`` is called the empirical process indexed by ``c``.
2. *asymptotically conituity*: The empirical process is called *asymptotically continuous* at ``\gamma`` if for all (arbitary, possibly random) sequences ``\left\{\gamma_{n}\right\}`` in ``\Gamma``, with ``\left\|\gamma_{n}-\gamma\right\|=o_{\mathbb{P}_{\theta}}(1)``, we have
    1. ``\left|\nu_{n}\left(\gamma_{n}\right)-\nu_{n}(\gamma)\right|=o_{\mathbb{P}_{\theta}}(1)``

PS: 
1. For verifying asymptotic continuity, there are various tools, which involve complexity assumptions on the map ``c \mapsto \psi_{c}``. This goes beyond the scope of these notes.
2. it is just like a property for continuity in analysis
3. I also remember the tail distribution for kernel in Gaussian process determines the degree of continuity at given point. (from GPML haha)

### Theorem 14.3.1: Asymptotic linearity of Z-estimator
1. Let ``\hat{\gamma}_{n}`` be the Z-estimator of ``\gamma``. Suppose 
    1. that ``\hat{\gamma}_{n}`` is a consistent estimator of ``\gamma`` 
    2. ``\nu_{n}(c):=\sqrt{n}\left(\hat{P}_{n}-P_{\theta}\right) \psi_{c}=\sqrt{n}\left(\dot{\hat{\mathcal{R}}}_{n}(c)-\dot{\mathcal{R}}(c)\right), c \in \Gamma`` is asymptotically continuous at ``\gamma``.
    3. ``M_{\theta}:=\left.\frac{\partial}{\partial c^{T}} \dot{\mathcal{R}}(c)\right|_{c=\gamma} \in \mathbb{R}^{p\times p}`` exists and full rank (positive definite)
    4. ``J_{\theta}:=P_{\theta} \psi_{\gamma} \psi_{\gamma}^{T} < \infty``
2. Then ``\hat{\gamma}_{n}`` is asymptotically linear, with inﬂuence function
    1. ``l_{\theta}=-M_{\theta}^{-1} \psi_{\gamma}``

#### Proof
1. By definition ``\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right)=0, \dot{\mathcal{R}}(\gamma)=0``
2. ``0 = \dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right) = \nu_{n}\left(\hat{\gamma}_{n}\right) / \sqrt{n}+\dot{\mathcal{R}}\left(\hat{\gamma}_{n}\right) = \nu_{n}\left(\hat{\gamma}_{n}\right) / \sqrt{n} + \left( \dot{\mathcal{R}}\left(\hat{\gamma}_{n}\right)-\dot{\mathcal{R}}(\gamma) \right)``
    1. The first term ``\nu_{n}\left(\hat{\gamma}_{n}\right) / \sqrt{n} = \nu_{n}\left( \gamma \right) / \sqrt{n} + o_{\mathbb{P}_{\theta}}(1) / \sqrt{n}`` by assumption (i) and (ii)
    2. The second term can be expand using Taylor expansion ``\dot{\mathcal{R}}\left(\hat{\gamma}_{n}\right)-\dot{\mathcal{R}}(\gamma) = M_{\theta}(\hat{\gamma}_{n} - \gamma ) + o(||\hat{\gamma}_{n} - \gamma|| )``
3. Put altogether we have ``0 =  \nu_{n}\left( \gamma \right) / \sqrt{n} + M_{\theta}(\hat{\gamma}_{n} - \gamma ) + o(||\hat{\gamma}_{n} - \gamma||)+ o_{\mathbb{P}_{\theta}}(1/ \sqrt{n}) ``
4. Then ``\hat{\gamma}_{n} - \gamma  = - M_{\theta}^{-1} \nu_{n}\left( \gamma \right) / \sqrt{n} + o(||\hat{\gamma}_{n} - \gamma||)+ o_{\mathbb{P}_{\theta}}(1/ \sqrt{n})``
    1. Term ``o(||\hat{\gamma}_{n} - \gamma||)`` does not affect the order analysis, can be omitted.
    2. By **CLT** ``\nu_{n}(c) = O_{\mathbb{P}_\theta}(1)``, therefore ``||\hat{\gamma}_{n} - \gamma|| = \mathcal{O}_{\mathbb{P}_{\theta}}(1 / \sqrt{n})``
5. Then ``\hat{\gamma}_{n} - \gamma  = - M_{\theta}^{-1} \nu_{n}\left( \gamma \right) / \sqrt{n} + o_{\mathbb{P}_{\theta}}(1/ \sqrt{n})``, which means asymptotic linearity.
    1. ``- M_{\theta}^{-1} \nu_{n}\left( \gamma \right) / \sqrt{n} = - M_{\theta}^{-1} \left(\dot{\hat{\mathcal{R}}}_{n}(\gamma)-\dot{\mathcal{R}}(\gamma)\right) = - M_{\theta}^{-1} \dot{\hat{\mathcal{R}}}_{n}(\gamma)``
    2. Therefore the influence function is ``l_{\theta}(x) = -M_{\theta}^{-1} \psi_{\gamma}(x)``
    3. The asymptotic covariance matrix is ``V_\theta = E_{\theta} l_{\theta}l_{\theta}^{\top} = M_{\theta}^{-1} J_{\theta} M_{\theta}^{-1}``


### Theorem 14.3.2: same as 14.3.1 skip

## 14.4 asymptotic normality of MLE
**Conclusion**: This section translate all the conclusion into MLE language under *regularity conditions* (differentiation of loss, etc).
1. loss: ``\rho_{\theta}(x) :=-\log p_{\theta}(x)``
2. empirical risk, MLE ``\hat{\theta}_{n}:=\underset{\tilde{\theta} \in \Theta}{\arg \max } \hat{P}_{n} \log p_{\tilde{\theta}}``
3. ``\psi_c(x) = \dot{\rho}_c(x) = - s_\theta(x)``, (def of score function)
4. ``M_{\theta}:=\left.\frac{\partial}{\partial c^{T}} \dot{\mathcal{R}}(c)\right|_{c=\gamma} = P_\theta \dfrac{\partial^2 \rho_c(x)}{\partial c \partial c^{\top}} = P_{\theta}\left(\frac{\ddot{p}_{\theta}}{p_{\theta}}-\frac{\dot{p}_{\theta}}{p_{\theta}} \frac{\dot{p}_{\theta}^{T}}{p_{\theta}}\right) = \left(\frac{\partial^{2}}{\partial \theta \partial \theta^{T}} 1\right)-P_{\theta} s_{\theta} s_{\theta}^{T}=-I(\theta)``, minus of Fisher information
5. influence function ``l_{\theta}=I(\theta)^{-1} s_{\theta}``
6. asymptotic covariance function ``V_\theta = I(\theta)^{-1}\left(P_{\theta} s_{\theta} s_{\theta}^{T}\right) I(\theta)^{-1}=I(\theta)^{-1}``
7. Overall ``\sqrt{n}\left(\hat{\theta}_{n}-\theta\right) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}\left(0, I^{-1}(\theta)\right)``.

## 14.5 Two examples of non-MLE loss
### Example 1 $\alpha$-quantail and median
1. In this example the loss is translational invariant ``\rho_c(x) := \rho(x-c)``
    1. where ``\rho(x):=(1-\alpha)|x| 1\{x<0\}+\alpha|x| 1\{x>0\}`` is a V-shaped loss and ``\alpha`` controls the slope of either side
2. The theoretical risk ``\mathcal{R}(c)`` can not be written explicit easily, however its derivative can
    1. by definition ``\psi_{c}(x) = \dot{\rho}_c(x) = -\alpha \mathrm{l}\{x>c\}+(1-\alpha)\{x<c\}``
    2. integration over ``\int \psi_{c}(x) dF(x)`` gives ``\dot{\mathcal{R}}(c)=P_{\theta} \psi_{c} = (1-\alpha)F(c) - \alpha(1-F(c)) =-\alpha+F(c)``
        1. ``F(x)`` is the distribution function for ``x``
    3. Therefore ``\dot{\mathcal{R}}(\gamma)=0, \text { for } \gamma=F^{-1}(\alpha)``, so ``\underset{c}{\arg \min } \mathcal{R}(c)=F^{-1}(\alpha)=: \gamma``
3. ``M_{\theta} =\left.\frac{d}{d c} \dot{\mathcal{R}}(c)\right|_{c=\gamma} =\left.\frac{d}{d c}(-\alpha+F(c))\right|_{c=\gamma} =f(\gamma)=f\left(F^{-1}(\alpha)\right)``
4. influence function ``l_{\theta}(x)=-M_{\theta}^{-1} \psi_{\gamma}(x)=\frac{1}{f(\gamma)}\{-1\{x<\gamma\}+\alpha\}``
5. The M-estimator ``\hat{\gamma}_{n}:=\underset{c}{\arg \min } \hat{\mathcal{R}}_{n}(c)= \hat{F}_{n}^{-1}(\alpha)`` also follows asymptotic normality
    1. ``\sqrt{n}\left(\hat{F}_{n}^{-1}(\alpha)-F^{-1}(\alpha)\right) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}\left(0, \frac{\alpha(1-\alpha)}{f^{2}\left(F^{-1}(\alpha)\right)}\right)``
6. When ``\alpha = 1/2`` the estimator is just the median!!!


### Example 2 Huber estimator
1. the loss is also assumed to be translational invariant ``\rho_{c}(x)=\rho(x-c)`` with
    1. ``\rho(x)= \begin{cases}x^{2} & |x| \leq k \\ k(2|x|-k) & |x|>k\end{cases}``
    2. therefore ``\dot{\rho}(x)= \begin{cases}2 x & |x| \leq k \\ +2 k & x>k \\ -2 k & x<-k\end{cases}``, and ``\psi_c(x) = - \dot{\rho}(x-c)``
2. Then ``\dot{\mathcal{R}}(c):=P_{\theta} \psi_{c}=-2 \int_{-k+c}^{k+c} (x-c) d F(x)-2 k[1-F(k+c)]+2 k F(-k+c)``
    1. with Leibniz's rule ``\dot{\mathcal{R}}(c) = 2\left\{\int_{c-k}^{c+k} F(x) d x-k\right\}``
    2. Then ``\gamma:=\underset{c}{\arg \min } P_{\theta} \rho_{c}`` is where ``\int_{\gamma-k}^{\gamma+k} F(x) dx - k = 0`` symmetric point.
3. ``M_{\theta}=\left.\frac{d}{d c} \dot{\mathcal{R}}(c)\right|_{c=\gamma}=2[F(k+\gamma)-F(-k+\gamma)]``
4. influence function ``l_{\theta}(x)=\frac{1}{[F(k+\gamma)-F(-k+\gamma)]} \begin{cases}x-\gamma & |x-\gamma| \leq k \\ +k & x-\gamma>k \\ -k & x-\gamma<-k\end{cases}``

## 14.6 Asymptotic relative efficiency
- *Definition* Let ``T_{n,1}`` and ``T_{n,2}`` be two estimators of ``\gamma``, that satisfy ``\sqrt{n}\left(T_{n, j}-\gamma\right) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}\left(0, V_{\theta, j}\right), j=1,2``.
    - Then ``\mathrm{e}_{2: 1}:=\frac{V_{\theta, 1}}{V_{\theta, 2}}`` is called the asymptotic relative eﬃciency of ``T_{n,2}`` with respect to ``T_{n,1}``.
- If ``\mathrm{e}_{2: 1} > 1``, the estimator ``T_{n,2}`` is asymptotically more eﬃcient than ``T_{n,1}``. An asymptotic $(1−\alpha)$-conﬁdence interval for $\gamma$ based on ``T_{n,2}`` is then narrower than the one based on ``T_{n,2}``.

### Examples
- For normal distribution, the mean is more efficient than the median.
- For Laplace distribution, the median is more efficient than the mean.

## 14.7 Asymptotic pivots
1. *Definition* An asymptotic pivot is a function ``Z_{n}(\gamma):=Z_{n}\left(X_{1}, \ldots, X_{n}, \gamma\right)`` of data ``X_{1:n}`` and parameter of interest ``\gamma=g(\theta)``, whose asymptotic distribution does not depend on the unknown parameter ``\theta``.
    1. namely ``Z_{n}(\gamma) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} Z, \forall \theta``
2. An asymptotic pivot can be used to construct approximate ``(1 − \alpha)``-conﬁdence intervals for ``\gamma``, and tests for ``H_{0}: \gamma=\gamma_{0}`` with approximate level ``\alpha``.

suppose we have an asymptotically normal estimator ``T_n`` of ``\gamma``, then ``\sqrt{n}\left(T_{n}-\gamma\right) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}\left(0, V_{\theta}\right), \forall \theta``. We can construct in following way

### ``1^{\mathrm{st}}`` asymptotic pivot
- assume
    1. ``V_{\theta}`` non-singular
    2. depends only on para of interest ``\gamma``
- then ``Z_{n, 1}(\gamma):=n\left(T_{n}-\gamma\right)^{T} V(\gamma)^{-1}\left(T_{n}-\gamma\right)`` has an asymptotic distribution of ``\chi^2``-distribution with ``p`` degrees of freedom.

### ``2^{\mathrm{nd}}`` asymptotic pivot
- assume ``\forall \theta`` one has a consistent estimator ``\hat{V}_{n}`` of ``V_{\theta}``,
- then the asymptotic pivot is ``Z_{n, 2}(\gamma):=n\left(T_{n}-\gamma\right)^{T} \hat{V}_{n}^{-1}\left(T_{n}-\gamma\right)``, it has an asymptotic distribution of ``\chi^2``-distribution with ``p`` degrees of freedom.
    - we can get this by Slutsky's lemma

### how to get an asymptotic consisten estimator ``\hat{V}_{n}`` of ``V_{\theta}``
1. (Method I) If 
    1. ``\hat{\theta}_{n}`` is a consistent estimator of ``\theta`` 
    2. ``\theta \mapsto V_{\theta}`` is continuous, 
    3. one may insert ``\hat{V}_{n}:=V_{\hat{\theta}_{n}}``
2. (Method II) If
    1. ``T_{n}=\hat{\gamma}_{n}`` is the Z-estimator of ``\gamma``, ``\gamma`` is the solution of ``P_{\theta} \psi_{\gamma}=0``
    2. then we try to plug into 
        1. ``V_{\theta}=M_{\theta}^{-1} J_{\theta} M_{\theta}^{-1}`` 
        2. where ``J_{\theta}=P_{\theta} \psi_{\gamma} \psi_{\gamma}^{T}``
        3. and ``M_{\theta} = P_{\theta} \dot{\psi}_{\gamma}``
    3. The plug-in is 
        1. first ``\hat{J}_{n}:=\hat{P}_{n} \psi_{\hat{\gamma}_{n}} \psi_{\hat{\gamma}_{n}}^{T}=\frac{1}{n} \sum_{i=1}^{n} \psi_{\hat{\gamma}_{n}}\left(X_{i}\right) \psi_{\hat{\gamma}_{n}}^{T}\left(X_{i}\right)``
        2. and ``\hat{M}_{n} = \frac{1}{n} \sum_{i=1}^{n} \dot{\psi}_{\hat{\gamma}_{n}}\left(X_{i}\right)``
    4. Finally we get ``\hat{V}_{n}:=\hat{M}_{n}^{-1} \hat{J}_{n} \hat{M}_{n}^{-1}``, a consistent estimator of ``V_\theta``

### 14.8Asymptotic Pivots for MLE
Alone with ``1^{\mathrm{st}}`` and  ``2^{\mathrm{nd}}`` asymptotic pivot, we can define a ``3^{\mathrm{rd}}`` Pivots, ``2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta):=2 \sum_{i=1}^{n}\left[\log p_{\hat{\theta}_{n}}\left(X_{i}\right)-\log p_{\theta}\left(X_{i}\right)\right]`` which is more natural.
#### Lemma 14.8.1
Under regularity, the following estimator is a pivot converging to a ``\chi^2`` distribution
```math
2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \chi_{p}^{2}, \forall \theta.
```
#### Sketch Proof
1. We expand ``\log p_{\hat{\theta}_{n}}\left(X\right) \approx \log p_{\theta}\left(X\right) + \partial_\theta \log p_{\theta}\left(X\right) (\hat{\theta}_{n} - \theta) + \partial^2_\theta \log p_{\theta}\left(X\right) (\hat{\theta}_{n} - \theta)^2/2 = \log p_{\theta}\left(X\right) + s_\theta(X) (\hat{\theta}_{n} - \theta) + \dot{s}_\theta(X)(\hat{\theta}_{n} - \theta)^2/2``
2. Therefore ``2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta) = 2n \left(\hat{\theta}_{n}-\theta\right)^{T} \hat{P}_{n} s_{\theta} + n\left(\hat{\theta}_{n}-\theta\right)^{\top}\left( \hat{P}_{n} \dot{s}_{\theta} \right) \left(\hat{\theta}_{n}-\theta\right)``
    1. For ``\hat{P}_{n} \dot{s}_{\theta}`` in the second term, we approximate it with ``\hat{P}_{n} \dot{s}_{\theta} \approx P_{\theta} \dot{s}_{\theta}=-I(\theta)``, the approxmation error results in higher order error in ithe equation, so we can neglect it.
    2. Therefore ``2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta) \approx 2 n\left(\hat{\theta}_{n}-\theta\right)^{T} \hat{P}_{n} s_{\theta}-n\left(\hat{\theta}_{n}-\theta\right)^{T} I(\theta)\left(\hat{\theta}_{n}-\theta\right)``
3. With the asymptotic linearity for MLE we have ``\hat{\theta}_{n}-\theta=I(\theta)^{-1} \hat{P}_{n} s_{\theta}+o_{\mathbb{P}_{\theta}}\left(n^{-1 / 2}\right)`` 
    1. then we can simplify ``2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta) \approx n\left(\hat{P}_{n} s_{\theta}\right)^{T} I(\theta)^{-1}\left(\hat{P}_{n} s_{\theta}\right)``
4. By the definition of Fisher information and **CLT**, ``\sqrt{n} \hat{P}_{n} s_{\theta} \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}(0, I(\theta))``
    1. We have ``2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \chi_{p}^{2}``

## 14.9 MLE for the multinomial distribution
not in exam, notes is straightfoward, skipped

it is just the calculation of three asymptotic pivot for multinomial distribution

## 14.10 Likelihood ratio test
1. In this section we want to test whether the true parameter follows some contrain ``R(\theta)=0``, where ``R(\theta) \in \mathbb{R}^{q}`` has full rank Jacobian at tru parameter ``\theta``.
    1. ``\dot{R}(\theta)=\left.\frac{\partial}{\partial \vartheta^{T}} R(\vartheta)\right|_{\vartheta=\theta}`` as rank ``q``.
2. To construct a test with null hypothesis of ``H_{0}: R(\theta)=0``, we construct an estimator ``\mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-\mathcal{L}_{n}\left(\hat{\theta}_{n}^{0}\right)``
    1. ``\hat{\theta}_{n}^{0}`` is solved by MLE **under constrain** (*e.g., Lagrange multiplier*) ``\hat{\theta}_{n}^{0}=\arg \max _{\vartheta \in \Theta: R(\vartheta)=0} \sum_{i=1}^{n} \log p_{\vartheta}\left(X_{i}\right)``
    2. ``\hat{\theta}_{n}`` is solved by MLE **without constrain**, ``\hat{\theta}_{n}=\arg \max _{\vartheta \in \Theta} \sum_{i=1}^{n} \log p_{\vartheta}\left(X_{i}\right)``

### Theorem 14.10.1 
Under regularity conditions, and if ``H_{0}: R(\theta)=0`` holds, we have ``2 \mathcal{L}_{n}(\hat{\theta}_{n})-2 \mathcal{L}_{n}(\hat{\theta}_{n}^{0}) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \chi_{q}^{2}``

### Proof
**Key Idea** The randomness of ``\hat{\theta}_{n}^{0}`` and ``\hat{\theta}_{n}`` comes from the difference of ``\mathbf{Z}_{n}:=\frac{1}{\sqrt{n}} \sum_{i=1}^{n} s_{\theta}\left(X_{i}\right)`` which is of order ``\mathcal{O}_{\mathbb{P}_\theta}(n^{-1/2})``. Also, its randomness is quantitively depictable. Although ``\hat{\theta}_{n}`` can be solved directly using Theorem 14.3.1, ``\hat{\theta}_{n}^{0}`` is still not explicit because of the contrain ``R(\theta)=0``. However we can still assume ``||\vartheta_n - \theta|| = \mathcal{O}_{\mathbb{P}_\theta}(n^{-1/2})`` , and approximate the risk up to second order ``\mathcal{R}(\vartheta_n) = D(A + B^{\top}(\vartheta_n - \theta) + (\vartheta_n - \theta)^{\top}C(\vartheta_n - \theta)/2 +  \mathcal{o}_{\mathbb{P}_\theta}(n^{-1}))``. Then we optimize over this approximate risk and get the approximate M-estimator. This approximation error is to the order of ``\mathcal{o}_{\mathbb{P}_\theta}(n^{-1})``, which does not affect the distribution of the test estimator.

1. using similar proccedure in Lemma 14.8.1 we approximate ``\mathcal{L}_{n}\left(\vartheta_{n}\right) := 2 \sum_{i=1}^{n}\left[\log p_{\vartheta_{n}}\left(X_{i}\right)-\log p_{\theta}\left(X_{i}\right)\right] = 2 \sqrt{n}\left(\vartheta_{n}-\theta\right)^{T} \mathbf{Z}_{n}-n\left(\vartheta_{n}-\theta\right)^{2} I(\theta)\left(\vartheta_{n}-\theta\right)+o_{\mathbf{P}_{\theta}}(1)`` which is in the form of ``n(A + B^{\top}(\vartheta_n - \theta) + (\vartheta_n - \theta)^{\top}C(\vartheta_n - \theta)/2 +  \mathcal{o}_{\mathbb{P}_\theta}(n^{-1}))``
2. The constrain can also be replaced with its linear approximation ``R\left(\vartheta_{n}\right)=\dot{R}(\theta)\left(\vartheta_{n}-\theta\right)+o_{\mathbf{P}_{\theta}}\left(n^{-1 / 2}\right) = \dot{R}(\theta)\vartheta_{n}  \triangleq 0``
3. Then the proposed test estimator is ``2 \mathcal{L}_{n}(\hat{\theta}_{n})-2 \mathcal{L}_{n}(\hat{\theta}_{n}^{0})  = \min_{\vartheta} \mathcal{L}_{n}\left(\vartheta_{n}\right)  - \min_{\vartheta: \dot{R}(\theta)\vartheta_{n}  \triangleq 0} \mathcal{L}_{n}\left(\vartheta_{n}\right)``
4. Using Lemma 12.5.1, and some calculation of ``\sigma^2`` we can say it has a ``\chi_{q}^{2}``-distribution.

## Contingency tables
This section is just an example showing 14.10 is meaningfull. An important part is the count of the degree of freedom. Not in exam, skipped.