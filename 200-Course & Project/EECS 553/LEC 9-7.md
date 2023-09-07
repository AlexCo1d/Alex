# Naive Bayes Classifier
By the Naive Bayes assumption, also using the notation in [[LEC 9-5#Notation|Notation]], we have:
$$
g_k(\boldsymbol{x})=\prod_{j=1}^dg_{kj}(x_j)
$$
Where $g_{kj}(x_{j})$ is the marginal $pdf$ of $X_{j}|Y=k$, then using the estimate in [[LEC 9-5#Plug-in estimation|Estimation]], we have:
$$
\begin{aligned} &\widehat{f}(x)=\text{argmax}_{k} \quad {\hat{\pi}_k}\widehat{g}_k(x)=\arg\max_k\pi_k\prod_{j=1}^dg_{kj}(x_j)\end{aligned}
$$
# Logistic Regression
focus on binary setting $Y\in \{0,1\}$:
LR produces an estimate $\widehat{\eta}(x)$ of :
$$
\eta(\boldsymbol{x}):=\Pr(Y=1\mid\boldsymbol{X}=\boldsymbol{x})
$$
As such,
$$\widehat{f}(x)=\begin{cases}
1 \quad & if \ \  \widehat{\eta}(x) \ >\frac{1}{2} \\
0\quad & if \ \  \widehat{\eta}(x)\ \leq\frac{1}{2}
\end{cases}$$

