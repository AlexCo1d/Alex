# Naive Bayes Classifier
By the Naive Bayes assumption, also using the notation in [[LEC 9-5#Notation|Notation]], we have:
$$
g_k(\boldsymbol{x})=\prod_{j=1}^dg_{kj}(x_j)
$$
Where $g_{kj}(x_{j})$ is the marginal $pdf$ of $X_{j}|Y=k$, then using the estimate in [[LEC 9-5#Plug-in estimation|Estimation]], we have:
$$
\begin{aligned} &\widehat{f}(x)=\text{argmax}_{k} \quad {\hat{\pi}_k}\widehat{g}_k(x)=\arg\max_k\pi_k\prod_{j=1}^dg_{kj}(x_j)\end{aligned}
$$
