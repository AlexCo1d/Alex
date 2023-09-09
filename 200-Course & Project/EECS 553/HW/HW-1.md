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
I use the following code to get the cost of time for every algorithm to predict for X_test
```python
min_n=0
max_n=2000
time_list={}
for n in range(max_n,min_n,-50):
    X_train=np.random.randn(n,2)
    X_test=np.random.randn(n,2)
    y_train=np.sign(np.random.randn(n))
    algorithm=['ball_tree','kd_tree', 'brute']
    k=5
    print('n:',n)
    for algo in algorithm:
        clf=KNeighborsClassifier(k,algorithm=algo)
        clf.fit(X_train,y_train)
        start_time=time.time()
        clf.predict(X_test)
        end_time=time.time()
        time_list[algo]=-start_time+end_time
        print("method:\t",algo,"  time:",-start_time+end_time)

    if (time_list['brute']==min(time_list.values())):
    print('true!',n)
    break

    print()
```

The results show that for n bigger than
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
Let G be the Gram matrix s.t. $G_{ij}=\left<\boldsymbol{x}_{i},\boldsymbol{x}_{j}\right>$ , so it is easy to tell that G is a symmetric matrix because $\forall i,j \ G_{ij}=G_{ji}$ . So 
Then $\forall$ vector y $\neq 0$, according to the matrix multiplication:
$$
y^TGy=\sum\limits_{i,j}^{n,n}y_{i}y_{j}G_{ij}=\sum\limits_{i,j}^{n,n}y_{i}y_{j}\left<\boldsymbol{x}_{i},\boldsymbol{x}_{j}\right>
$$
Where $y_{i}$ denotes the i-th component of vector y, which is a <u>number</u>.
From the bi-linear property of inner product:
$$
\sum\limits_{i,j}^{n,n}y_{i}y_{j}\left<\boldsymbol{x}_{i},\boldsymbol{x}_{j}\right>=\sum\limits_{i,j}^{n,n}\left<y_{i}\boldsymbol{x}_{i},y_{j}\boldsymbol{x}_{j}\right>=\left<\sum\limits_{i=1}^{n}y_{i}\boldsymbol{x}_{i},\sum\limits_{j=1}^{n}y_{j}\boldsymbol{x}_{j}\right>=\left|\left|\sum\limits_{i=1}^{n}y_{i}\boldsymbol{x}_{i}\right|\right|^{2}\geq 0
$$

Based on the definition of PSD matrix, gram is a PSD matrx.