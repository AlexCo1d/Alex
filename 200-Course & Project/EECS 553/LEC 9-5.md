# Bayes Classifier
## Probabilistic Setting
$X \in \mathbb{R}^{d}$ is a vector, and y is label
We need to characterize the joint distribution $(X,y)$
-  marginal distribution Y, and conditional distribution X given $Y=y$
		Then $P(y,x)=P(x|y)\cdot P(y)$
-  marginal distribution X, and conditional distribution Y given $X=x$
		Then $P(y,x)=P(y|x)\cdot P(x)$

```ad-tip
title: marginal distribution
$$
P(X)=\sum_{i=1}^kP(X,y_i)=\sum_{i=1}^kP(X|y_i)\times P(y_i)
$$
```

So we have
$$
P(y_i|X)=\frac{P(X|y_i)\times P(y_i)}{P(X)}
$$
Where we name $P(y_{i}|\boldsymbol{X})$ posterior probability; $P(\boldsymbol{X}|y_{i})$ is likelihood; $P(y_{i})$ is class prior probability.

```ad-note
if it is a <u>naive bayes</u>, then it assume that all component in vector $\boldsymbol{x}$ is condition independent, so $P(\boldsymbol{x})=\Pi_{i=1}^{k}P(\boldsymbol{x}^{(i)})$
```

## Notation
- $\eta_k(\boldsymbol{x})= Pr(Y=k|X=x)$,
- $g(x)=pdf \ of \ X$,
- $g_k(x)=pdf \ of \ X, \ given \ Y=k$,
- $\pi_k=Pr(Y=k)$

## Joint distribution
$$g(\boldsymbol{x})=\pi_1 g_1 (\boldsymbol{x})+\pi_2 g_2 (\boldsymbol{x}) 
$$
$$
\eta_1 (\boldsymbol{x})=\frac{\pi_1 g_1 (\boldsymbol{x})}{\pi_1 g_1 (\boldsymbol{x})+\pi_2 g_2 (\boldsymbol{x})} 
$$
## Bayes classifier 
Bayes classifier is a function $f(X): X\in\mathbb{R}^{d} \rightarrow \{1,\ldots, K\}$, given a joint distribution of $\{X, Y\}$

And the error, or risk is $R(f)=P(f(x)\neq y)$, which measure the performance of the bayes classifier. We call it _risk_ . R* is the smallest risk,
Also, we have:
$$\mathop{arg \ min}\limits_{1\leq k\leq K} \ R(f) \  \Leftrightarrow \ \mathop{arg \ max}\limits_{1\leq k\leq K} \ \eta_k(\boldsymbol{x}) \Leftrightarrow \mathop{arg \ max}\limits_{1\leq k\leq K}\ \pi_{k}g_{k}(x)$$
Because $g (x)$ is a constant, called *evidence*.
To use this classifier, just compare $\pi g_{1}(x)$ and $\pi g_{0}(x)$, to get the maximum.

# Linear Discriminant Analysis
## Plug-in estimation
Because in ML, we don't have the exact data of $\pi_k,g_k(x),\eta_k(x)$, so we could only estimate the quantities in the formula, get a classifier.
From the maximum likelihood estimate:
$$
\begin{aligned}
\widehat{\pi}_{k}& \begin{aligned}&=\frac{n_k}n,\quad\quad\quad n_k=|\{i:y_i=k\}|\end{aligned}  \\
\widehat{\boldsymbol{\mu}}_k& =\frac1{n_k}\sum_{i:y_i=k}\boldsymbol{x}_i  \\
\widehat{\Sigma}& \begin{aligned}=\frac1n\sum_{i=1}^n(\boldsymbol{x}_i-\widehat{\boldsymbol{\mu}}_{y_i})(\boldsymbol{x}_i-\widehat{\boldsymbol{\mu}}_{y_i})^T\end{aligned} 
\end{aligned}
$$
## Gaussian case
$$
f_k(x)=\frac1{(2\pi)^{l/2}|\boldsymbol{\Sigma}_k|^{1/2}}e^{-\frac12(x-\mu_k)^T\boldsymbol{\Sigma}_k^{-1}(x-\mu_k)}
$$
Where l is the total classes of Y.
Use the compare way in a *log form*, and we can get:
$$
b+2(\mu_{1}-\mu_{2})^{\top}\Sigma^{-1}x >0
$$
So for binary setting $Y\in \{0,1\}$:
The LDA classifier is when using the [[#Plug-in classifier]]
$$
\widehat{f}(\boldsymbol{x})=\operatorname{sign}(\boldsymbol{w}^T\boldsymbol{x}+b)
$$ where
$$
\begin{aligned}\boldsymbol{w}&=\widehat{\boldsymbol{\Sigma}}^{-1}(\widehat{\boldsymbol{\mu}}_1-\widehat{\boldsymbol{\mu}}_{-1})\\b&=\log(\widehat{\pi}_1/\widehat{\pi}_{-1})+\frac12(\widehat{\boldsymbol{\mu}}_{-1}^T\widehat{\boldsymbol{\Sigma}}^{-1}\widehat{\boldsymbol{\mu}}_{-1}-\widehat{\boldsymbol{\mu}}_1^T\widehat{\boldsymbol{\Sigma}}^{-1}\widehat{\boldsymbol{\mu}}_1).\end{aligned}
$$
When could see that it is a linear classifier in a *d-dimension hyperplane*. For more detail, see [LDA]( https://esl.hohoweiya.xyz/04-Linear-Methods-for-Classification/4.3-Linear-Discriminant-Analysis/index.html)

