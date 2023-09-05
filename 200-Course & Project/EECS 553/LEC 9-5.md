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

And the error, or risk is $err(f)=P(f(x)\neq y)$, which measure the performance of the bayes classifier. Also, we have:
$$\mathop{arg \ min}\limits_{1\leq k\leq K} \ err(f) \  \Leftrightarrow \ \mathop{arg \ max} \ \eta_k(\boldsymbol{x})=P(y=k|\boldsymbol{x})$$
# Plug-in classifier
Because in ML, we don't have the exact data of $\pi_k,g_k(x),\eta_k(x)$, so we could only estimate the quantities in the formula, get a classifier.
# Linear Discriminant Analysis
