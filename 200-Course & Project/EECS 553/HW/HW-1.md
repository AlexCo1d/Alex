Yuanhao Zou,  yuanhaoz@umich.edu
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
```output
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
max_n=100000
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

The results show that for larger n, such as those in the range of 1500 to 100000, it takes significantly longer to infer the brute algorithm than the other two algorithms. At the same time, I observed that when n is in the range of 1400 to 1000, the three algorithms run in about the same time. However, these measured times are always fluctuating and I could not get the exact minimum value. Therefore I roughly observed a minimum n of 1400. In the following code block is part of my program above's output.
```output
n: 1500
method:	 ball_tree   time: 0.08685111999511719
method:	 kd_tree   time: 0.08310794830322266
method:	 brute   time: 0.3519430160522461

n: 1450
method:	 ball_tree   time: 0.07758688926696777
method:	 kd_tree   time: 0.06316518783569336
method:	 brute   time: 0.14694452285766602

n: 1400
method:	 ball_tree   time: 0.04186415672302246
method:	 kd_tree   time: 0.04026007652282715
method:	 brute   time: 0.05213451385498047

n: 1350
method:	 ball_tree   time: 0.040220022201538086
method:	 kd_tree   time: 0.05111074447631836
method:	 brute   time: 0.04634356498718262

n: 1300
method:	 ball_tree   time: 0.04042410850524902
method:	 kd_tree   time: 0.03107285499572754
method:	 brute   time: 0.04288458824157715

n: 1250
method:	 ball_tree   time: 0.03975653648376465
method:	 kd_tree   time: 0.033684492111206055
method:	 brute   time: 0.04698586463928223

n: 1200
method:	 ball_tree   time: 0.04727506637573242
method:	 kd_tree   time: 0.03237748146057129
method:	 brute   time: 0.061133384704589844

n: 1150
method:	 ball_tree   time: 0.03566122055053711
method:	 kd_tree   time: 0.027804851531982422
method:	 brute   time: 0.03971266746520996

n: 1100
method:	 ball_tree   time: 0.039412736892700195
method:	 kd_tree   time: 0.027874469757080078
method:	 brute   time: 0.043331146240234375

n: 1050
method:	 ball_tree   time: 0.030924558639526367
method:	 kd_tree   time: 0.034847259521484375
method:	 brute   time: 0.03602409362792969

n: 1000
method:	 ball_tree   time: 0.03258514404296875
method:	 kd_tree   time: 0.024677753448486328
method:	 brute   time: 0.03885793685913086

n: 950
method:	 ball_tree   time: 0.02947378158569336
method:	 kd_tree   time: 0.023334026336669922
method:	 brute   time: 0.03251385688781738

n: 900
method:	 ball_tree   time: 0.030408859252929688
method:	 kd_tree   time: 0.03508472442626953
method:	 brute   time: 0.03603768348693848
```

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

Based on the definition of PSD matrix, gram is a PSD matrix.
$\square$ 

# Question 3

Because bayes classifier $h^{*}(x)$ achieves the lowest risk for $R(h^{*})=R^{*}$, we have:
$$h^{*}(x)=
\begin{cases}
1 & \eta(x)\geq \frac{1}{2}\\
-1 & \eta(x)<\frac{1}{2}
\end{cases}
$$
So 
$$
h^{*}(x)=sign(\eta(\boldsymbol{x})- \frac{1}{2})=sign(2\eta(\boldsymbol{x})-1)\tag{3.1}
$$
According to the formula in ***lecture notes***, we have 
$$\begin{align*}
R(h) & =\mathbb{E}_{\boldsymbol{X}}\left[1_{\{h(x)\neq y\}}\right]\\\\
& =\mathbb{E}_{\boldsymbol{X}}\left[\mathbb{E}_{Y|\boldsymbol{X}}\left[1_{\{h(x)\neq y\}}\right]\right]\\\\
& =\mathbb{E}_{\boldsymbol{X}}\left[\sum\limits_{k=-1,1}\left(\eta_{k}(x)\cdot 1_{\{h(x)\neq k\}}\right)\right] \\

\end{align*}
$$
Because there are only two label $Y=\{1,-1\}$, thus we have $\eta_{1}(x)+\eta_{-1}(x)=1$
, and we denote $\eta(\boldsymbol{X})=\eta_{1}(x)$ , $\eta_{-1}(x)=1-\eta(\boldsymbol{X})$. So:
$$\begin{align*}
R(h) &= \mathbb{E}_{\boldsymbol{X}}\left[\eta(\boldsymbol{X})\cdot 1_{\{h(x)=-1,k=1\}}+(1-\eta(\boldsymbol{X}))\cdot 1_{\{h(x)=1,k=-1\}} \right] \\\\
&=\mathbb{E}_{\boldsymbol{X}}\left[\eta(\boldsymbol{X})\cdot 1_{\{h(x)=-1\}}+(1-\eta(\boldsymbol{X}))\cdot 1_{\{h(x)=1\}} \right] \tag{3.2}\end{align*}

$$
From
$$
1_{\{h(x)=1\}}+1_{\{h(x)=-1\}}=1 \Rightarrow \mathbb{E}_{\boldsymbol{X}}\left[1-\eta(\boldsymbol{X})+(2\eta(\boldsymbol{X})-1)\cdot 1_{\{h(x)=-1\}} \right] 
$$
Following the same derivation, we can get:
$$
R(h^{*})=\mathbb{E}_{\boldsymbol{X}}\left[1-\eta(\boldsymbol{X})+(2\eta(\boldsymbol{X})-1)\cdot 1_{\{h^{*}(x)=-1\}} \right] \tag{3.3}
$$
Combining (3.2) and (3,3) ,we get
$$\begin{align*}
R(h)-R(h^{*}) &=\mathbb{E}_{\boldsymbol{X}}\left[(2\eta(\boldsymbol{X})-1)\cdot (1_{\{h(x)=-1\}}-1_{\{h^{*}(x)=-1\}}) \right]\\
\end{align*}
$$
We notice that, 
$$
\mathbf{1}_{\{h(\boldsymbol{x})=-1\}}-\mathbf{1}_{\{h^*(\boldsymbol{x})=-1\}}=
\begin{cases} 
1&\mathrm{~if~}h(\boldsymbol{x})=-1,h^*(\boldsymbol{x})=1\\
-1&\mathrm{~if~}h(\boldsymbol{x})=1,h^*(\boldsymbol{x})=-1\\
0&\mathrm{~if~}h(\boldsymbol{x})=h^*(\boldsymbol{x})&
\end{cases}
$$
When $h^{*}(x)=1,2\eta(\boldsymbol{X})-1\geq 0$ , and when $h^{*}(x)=-1,2\eta(\boldsymbol{X})-1< 0$, thus we use the relationship between $h(x)$ and $h^{*}(x)$ to represent the formula by:
$$
(2\eta(\boldsymbol{X})-1)\cdot (1_{\{h(x)=-1\}}-1_{\{h^{*}(x)=-1\}})=\left|(2\eta(\boldsymbol{X})-1)\right|\cdot 1_{\{h(x)\neq h^*(x)\}}
$$
Because (3.1), we have proved that
$$
R(h)-R^*=\mathbb{E}_{\boldsymbol{X}}\left[\left|2\eta(\boldsymbol{X})-1\right|1_{\{h(\boldsymbol{X})\neq\operatorname{sign}(2\eta(\boldsymbol{X})-1)\}}\right].
$$
$\square$ 
[ref](https://homepages.warwick.ac.uk/staff/Martin.Lotz/files/learning/lect2.pdf)

# Question 4
## (a)

$$
\begin{align*}
&(x-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\boldsymbol{x}-\boldsymbol{\mu})\leq r^2\\
\Leftrightarrow \ & (x-\boldsymbol{\mu})^{T}U\Lambda U^T(\boldsymbol{x}-\boldsymbol{\mu})\leq r^2
\end{align*}
$$
Let y= $U^T(\boldsymbol{x}-\boldsymbol{\mu})$, $y_{1},y_{2}$ be 2 component of the vector y, then 
$$
\begin{align*}
(x-\boldsymbol{\mu})^{T}U\Lambda^{-1} U^T(\boldsymbol{x}-\boldsymbol{\mu})
&=  y^{T}\Lambda^{-1} y\\
&=  \frac{y_1^2}{\lambda_1}+\frac{y_2^2}{\lambda_2}\leq r^2 
\end{align*}
$$
Since $U=\left[\begin{array}{cc}\cos\theta&-\sin\theta\\\sin\theta&\cos\theta\end{array}\right],\theta=\frac{\pi}{4}$,   $U^{T}=\left[\begin{array}{cc} \frac{\sqrt{2}}{2}&\frac{\sqrt{2}}{2}\\-\frac{\sqrt{2}}{2}&\frac{\sqrt{2}}{2}\end{array}\right]$

we have $y_{1}=\frac{\sqrt{2}}{2}(x_{1}-1)+\frac{\sqrt{2}}{2}(x_{2}-1)$, and $y_2=-\frac{\sqrt{2}}{2}(x_{1}-1)+\frac{\sqrt{2}}{2}(x_{2}-1)$
So the scratch is the following figure:

![[Q4.1.png|figure]]
Where $O$ denotes the origin point of $x_{1},x_2$ coordinate system, while $O'$ denotes the origin point of $y_{1},y_2$ coordinate system. The angle between the 2 coordinate systems are $\frac{\pi}{4}$ 

## (b)
Let $\boldsymbol{Y}=\Sigma^{- \frac{1}{2}}(X-\mu)$, Y is a random variable with 2 component each $\boldsymbol{y}$
then
$$
(x-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\boldsymbol{x}-\boldsymbol{\mu})=Y^{T}Y
\\
\Rightarrow C:=\{\boldsymbol{y}\ |\ y^{T}y\leq r^{2}\}$$
Also, because $X\sim\mathcal{N}(\boldsymbol{\mu},\boldsymbol{\Sigma})$, according to the properties of gaussian distribution's linearity we have
$$\begin{align*}
\boldsymbol{Y}=\Sigma^{- \frac{1}{2}}(X-\mu)
\Rightarrow \boldsymbol{Y}\sim \mathcal{N}(0,\Sigma^{- \frac{1}{2}}\Sigma\Sigma^{- \frac{1}{2}})\Leftrightarrow\boldsymbol{Y}\sim(0,I)
\end{align*}$$
From the definition of [chi-square distribution](https://en.wikipedia.org/wiki/Chi-squared_distribution), $Y^{T}Y=Y_{1}^{2}+Y_{2}^{2}$ satisfy a k=2 chi-squared distribution, where k is the degree of freedom. So we have:
$$Pr(X\in C)=Pr(Y_{1}^{2}+Y_{2}^{2}\leq r^{2})=F_{\chi^2}(r^2)$$
If $r=\sqrt{2}$, then $Pr(X\in C)=F_{\chi^2}(2)=0.632121$

# Question 5
## (a)
Proof:
$$
\begin{align*}
g(t\boldsymbol{x}+(1-t)\boldsymbol{y})&=f(A(t\boldsymbol{x}+(1-t)\boldsymbol{y})+\boldsymbol{b})\\
&=f(t(A \boldsymbol{x+b})+(1-t) (A \boldsymbol{y}+\boldsymbol{b}))
\end{align*}
$$ Since function $f$ is convex, so 
$$
\begin{align*}
f(t(A \boldsymbol{x+b})+(1-t) (A \boldsymbol{y}+\boldsymbol{b}))&\leq tf(A \boldsymbol{x+b})+(1-t)f(A \boldsymbol{y+b})\\
&=tg(\boldsymbol{x})+(1-t)g(\boldsymbol{y})
\end{align*}
$$
Thus
$$
g(t\boldsymbol{x}+(1-t)\boldsymbol{y})\leq tg(\boldsymbol{x})+(1-t)g(\boldsymbol{y})
$$
$g(x)$ is a convex function, $\square$

## (b)

