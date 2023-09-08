Yuanhao Zou
yuanhaoz@umich.edu
# Question 1
## (a)
I use the following code to compare different algorithm's cost of time.
```python
import time  
import numpy as np  
from sklearn.neighbors import KNeighborsClassifier  
  
np.random.seed(1000)  
k = 5  
#  
n_list = [1000, 10000]  
for n in n_list:  
    X_train = np.random.randn(n, 2)  
    y_train = np.sign(np.random.randn(n))  
    algorithm = ['ball_tree', 'kd_tree', 'brute']  
  
    print('n:', n)  
    for algo in algorithm:  
        clf = KNeighborsClassifier(k, algorithm=algo)  
        start_time = time.time()  
        clf.fit(X_train, y_train)  
        end_time = time.time()  
  
        print("method:\t", algo, "  time:", -start_time + end_time)  
    print()
```

The result is here. We can see in training stage, the brute algorithm is the fastest one.
```
n: 1000
method:	 ball_tree   time: 0.007141828536987305
method:	 kd_tree   time: 0.0018720626831054688
method:	 brute   time: 0.0006821155548095703

n: 10000
method:	 ball_tree   time: 0.005206108093261719
method:	 kd_tree   time: 0.007337093353271484
method:	 brute   time: 0.0011408329010009766
```

## (b)

# Question 2
## (a)
Because A is a symmetric matrix, thus it could be factorized as:
$$
A=Q\Lambda Q^{-1}=Q\Lambda Q^T
$$
Where Q is an orthogonal matrix s.t.  $Q^{\top}=Q^{-1}$, and $\Lambda$ is a diagonal matrix that consists of each of the eigenvalues $\lambda_{1},\lambda_{2},\ldots,\lambda_{n}$ of $A$
$$Q^{\top}=Q^{-1} \Leftrightarrow Q^{\top}Q=I$$
$$\Rightarrow x^{T}Ax=x^{T}(Q^{T}Q)A(Q^{T}Q)x=x^{T}Q^{T}\Lambda Qx$$
Let $x^{T}Q^{T}=y^{T}$, so $y=Qx$
Because $\Lambda$ is a diagonal matrix, we have:
$$
y^{T}\Lambda y=\sum\limits_{i=1}^{n}\lambda_{i}y_{i}^{2}
$$
Where $y_{i}$ is the i-th component of vector $\boldsymbol{y}$ 
Because $\forall\lambda_{i}>0$ , thus  $\sum\limits_{i=1}^{n}\lambda_{i}y_{i}^{2}>0$ $\Rightarrow x^{T}Ax=y^{T}\Lambda y>0$ 
$\square$ 

## (b)
Let G be the Gram matrix s.t. $G_{ij}=<\boldsymbol{x}_{i},\boldsymbol{x}_{j}>$ , so it is easy to tell that G is a symmetric matrix because $\forall i,j \ G_{ij}=G_{ji}$ 
Then for vector y $\neq 0：$
$$
y^TGy=
$$

