# Chpater 12 The Linear Model

## Exam 
- LS estimator 
    - deﬁnition 
- Lemma 12.3.1+ proof
- lemma on prediction error gaussian noise should be able to prove
- to test a particular hypothesis, how you would carry out the test

## intro
- introducion of Problem
  - the oracal way of data generation is $y = f(x) + \epsilon$, $y\in \mathbb{R}$ and $x\in \mathbb{R}^{p\times 1}$. We want to use a linear model $y = \beta^{\top}x$ to estimate the relation $f(\cdot)$.
  - the formal problem is ``\hat{\beta} = \underset{\beta}{\arg\min} ||Y-X\beta||^2``.
- the solution is $\hat{\beta} = (X^{\top}X)^{-1}X^{\top}Y$, and the prediction $\hat{Y} = X(X^{\top}X)^{-1}X^{\top}Y$.
  - The transformation $P_{X} =X(X^{\top}X)^{-1}X^{\top}$ is a projection matrix in $\mathbb{R}^{n\times n}$ since that $P_{X}P_{X} = P_{X}$, the solution $\hat{\beta}$ can be though of as the closest vector in this projected subspace.
  - if we do a SVD on $X$, the projection matrix can be simplified. Suppose $X\in\mathbb{R}^{n\times p}$ is full rank $p$. then $\underset{n\times p}{X} = \underset{n\times p}{P}\times\underset{p\times p}{\mathrm{diag}\{\phi_i\}}\times\underset{p\times p}{Q}$, where $QQ^{\top} = Q^{\top}Q = I_{p\times p}$, and $P = \{p_1, p_2, \cdots, p_p\}$ and $p_i^{top}p_j = \delta_{i,j}$ (Or in matrix form, $P^{\top} P = I_{p\times p}$).
    - then the projection matrix is $P_{X} =X(X^{\top}X)^{-1}X^{\top} =PP^{\top}$

## Lemma 12.3.1 and Lemma 12.3.2.
-  Since we are assuming independent identical gaussian noise for each data point $\epsilon \sim \mathcal{N}(0,\sigma^2)$, some for interesting statement can be found.
  - the estimator $\hat{\beta}$ is gaussian, with mean $\mathbb{E}\hat{\beta} = \beta^{*} = (X^{\top}X)^{-1}X^{\top} f(X)$, (in some lemma, we assume the oracal function $f(\cdot)$ is also a linear function $f(x) = x^{\top}\beta$), and covariance $\mathrm{Cov}\hat{\beta} = \sigma^2 (X^{\top}X)^{-1}$. (Lemma 12.3.1 (i))
  - the norm w.r.t best prediction ``||X(\hat{\beta} - \beta^{*})||^2`` follows a $\chi^2_p$-distribution (Lemma 12.3.2 (ii)), and its mean is ``\mathbb{E}||X(\hat{\beta} - \beta^{*})||^2 = p\sigma^2``
    - the proof trick lies in that $X(\hat{\beta} - \beta^{*}) = P_X\epsilon$, and $\epsilon$ is a spherically symmetric random variable that is also iid under orthonormal transformation. Therefore $P_x\epsilon$ is also an iid gaussian of $\mathcal{N}(0,\sigma^2)$ with dimension of $\mathbb{R}^{p \times 1}$.
    - the mean square error can be decomposed as ``\mathbb{E}||X\hat{\beta} - f(X))||^2 = \mathbb{E}||X(\hat{\beta}-\beta^{*}))||^2 + \mathbb{E}||X\beta^{*} - f(X))||^2 = p\sigma^2 + \mathbb{E}||X\beta^{*} - f(X))||^2`` (Lemma 12.3.1(iii))
      - this lemma is just a use of Pythagoras's rules. No need to use zero mean in the intersection term.
      - ``\mathbb{E}||X\beta^{*} - f(X))||^2`` is the error by linear assumption
  - As a further extension of Lemma 12.3.2(ii), if we assume the oracal is also linear, $f(x) = x^{\top}\beta$. Then $Y - f(X) = \epsilon$, we can rewrite it as $Y - f(X) = Y - X\hat{\beta} + X\hat{\beta} - X\beta = \epsilon \in \mathbb{R}^{n\times 1}$. Since we know that $X(\hat{\beta} - \beta) = P_{X}\epsilon$, therefore $Y-X\hat{\beta} = (I_{n\times n}-P_{X})\epsilon = P_{X}^{\perp}\epsilon$. Since $P_x\epsilon$ and $P_{X}^{\perp}\epsilon$ are independent, we can say that $Y-X\hat{\beta}$ and $X(\hat{\beta}-\beta)$ are independent
    - this gives a corollary. If we hypothesize on that $f(\cdot)$ is linear and the coefficient is $\beta_0$ ($\mathcal{H_0}: \beta = \beta_0$), then by this hypothesis, ``||X(\hat{\beta} - \beta_0)||^2 / \sigma_0^2`` follows a $\chi^2_p$ distribution (when $\sigma_0$ is known), this can be used to construct test  $\phi$ that we reject ``\mathcal{H_0}`` if ``{||X(\hat{\beta} - \beta_0)||^2}/{\sigma_0^2} > G^{-1}(1-\alpha)``.
    - when $\sigma_0^2$ is unknown, we use estimator ``\hat{\sigma}^2 = ||Y-X\hat{\beta}||^2/(n-p)`` to estimate. By the corollary we know that $\hat{\sigma}^2$ and ``||X(\hat{\beta} - \beta_0)||^2`` are independent, so that we can define the new distribution $F_{p,n-p}$ much more easily.

## Testing constrains on coeficient
- In this section we want to make test on wheter the coefficient follows some constrains s.t. $B\beta = 0$.
  - For that we need to show that what is the MLE solution behave like.
  - Lemma 12.4.1: $\max _{a \in \mathbb{R}^{p}: B a=0}\left\{2 a^{T} z-a^{T} a\right\}=z^{T} z-z^{T} B^{T}\left(B B^{T}\right)^{-1} B z$.
    - this can be proved using the fact that the restricted $a$ can be rewritten in from of $a=P_B \alpha$ where $P_B= I - B^{\top}(BB^{\top})^{-1}B$ and $\alpha$ being arbitary.
  - Lemma 12.4.2 $\max _{a \in \mathbb{R}^{p} ; B a=0}\left\{2 a^{T} z-a^{T} V a\right\}=z^{T} V^{-1} z-z^{T} V^{-1} B^{T}\left(B V^{-1} B^{T}\right)^{-1} B V^{-1} z$
    - This can be prove using lemma 12.4.1 and with transformation that $a^{*} = V^{1/2}a,B^{*}=BV^{-1/2},z^*=V^{-1/2}z$.
  - From Lemma 12.4.2 we arive at corollary 12.4.1, define $L(a):=2 a^{T} z-a^{T} V a$, then the maxium with and without constrain has a difference of $\max _{a} L(a)-\max _{a: B a=0} L(a)=z^{T} V^{-1} B^{T}\left(B V^{-1} B^{T}\right)^{-1} B V^{-1} z$.
- Lemma 12.5.1, We want to test wheter our solution is under this constrain ``\hat{\beta}_{0}:=\arg \min _{b \in \mathbb{R}^{p}: B b=0}\|Y-X b\|_{2}^{2}``, this lemma tells us that the quantity ``\left[ \left\|Y-X \hat{\beta}_{0}\right\|_{2}^{2}-\|Y-X \hat{\beta}\|_{2}^{2} \right]/\sigma^2`` is a $\chi^2_q$-distribution under this hypothesis (where $q$ is the rank of $B\in \mathbb{R}^{q\times p}$), base on this distribution we can construct test.
  - The proof is direct, first we write the loss in quadratic form ``\|Y-X b\|^{2}=\|\epsilon\|^{2}-2 \epsilon^{T} X(b-\beta)+(b-\beta)^{T} X^{T} X(b-\beta)``
  - Then the quantity $\max _{a} L(a)-\max _{a: B a=0} L(a)=z^{T} V^{-1} B^{T}\left(B V^{-1} B^{T}\right)^{-1} B V^{-1} z$ in this specific problem is $Z^{T}\left(B\left(X^{T} X\right)^{-1} B^{T}\right)^{-1} Z$, where $Z:=B\left(X^{T} X\right)^{-1} X^{T} \epsilon$.
  - we can varify that the matrix $\left(B\left(X^{T} X\right)^{-1} B^{T}\right)^{-1}$ in the quadratic form is just the inverse of $\mathrm{{Cov}}Z$ therefore this quadratic form can be transformed into sumation of $q$ random variable of $\mathcal{N}(0,1)$. (This corollary is obvious, but it is also proved in the beginning of 12.2)