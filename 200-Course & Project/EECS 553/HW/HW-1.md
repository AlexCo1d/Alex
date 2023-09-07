# Question 1
## (a)
```python
np.random.seed(1000)
k=5
#
n_list=[1000,10000]
for n in n_list:
	X_train=np.random.randn(n,2)
	y_train=np.sign(np.random.randn(n))
	algorithm=['ball_tree','kd_tree', 'brute']

	print('n:',n)
	for algo in algorithm:
		clf=KNeighborsClassifier(k,algorithm=algo)
		start_time=time.time()
		clf.fit(X_train,y_train)
		end_time=time.time()
      
	print("method:\t",algo,"  time:",-start_time+end_time)
  
	print()```


## (b)
