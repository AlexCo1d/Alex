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
$$\mathop{arg \ min}\limits_{1\leq k\leq K} \ R(f) \  \Leftrightarrow \ \mathop{arg \ max} \ \eta_k(\boldsymbol{x}) \Leftrightarrow arg \ max\ \pi_{k}g_{k}(x)$$
Because $g (x)$ is a constant, called *evidence*.
# Plug-in classifier
Because in ML, we don't have the exact data of $\pi_k,g_k(x),\eta_k(x)$, so we could only estimate the quantities in the formula, get a classifier.

# Linear Discriminant Analysis
