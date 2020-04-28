### Transition and sensor model

Transition Model定义了给出过去状态下, 当前状态的概率分布, 即 
$$
P(X_{t}|X_{0:t-1})
$$
这里, 我们引入Markov assumption (First Order Markov Process), 即当前状态只取决于上一个状态, 即
$$
P(X_{t}|X_{t-1})
$$



should use central parameters


### Discrete Variables

HMM

### Continous Variables

Kalman filtering

### Dynamic Bayesian network(DBN)

DBN是一个概率模型, 一般来说, 每一段DBN都可以有任意个状态变量Xt和观测变量Et

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/5/56/R%C3%A9seau_bay%C3%A9sien_dynamique.svg/661px-R%C3%A9seau_bay%C3%A9sien_dynamique.svg.png)



### Exact inference in DBNs







### Approximate Inference in DBNs

Approximation algorithms

* Likelihood weighting
* Markov Chain Monte Carlo

### Particle filter

![particle_filter_alog](/home/yang/Desktop/github/blog/phd/particle_filter_alog.png)

<https://blog.csdn.net/piaoxuezhong/article/details/78619150>

#### Bayes filtering

两个步骤

- 预测
- 更新

假设已知k-1时刻的概率密度函数 
$$
p(x_{k-1}|y_{1:k-1})
$$
预测: 由上一时刻的概率密度函数p(xk-1|y1:k-1)得到p(xk|y1:k-1)  (即先验概率)

![predict](/home/yang/Desktop/github/blog/phd/predict.png)

更新: 由p(xk|y1:k-1)得到后验概率p(xk|y1:k). 这个后验概率才是真正有用的东西, 上一步还只是预测, 这里多了k时刻的测量, 对上面的预测在进行修正, 就是滤波了, 形成递推.

![posteroi](/home/yang/Desktop/github/blog/phd/post.png)

#### Monte Carlo Sampling

假设我们能从一个目标概率分布p(x)中采样得到一系列的样本粒子(particles), x1,...xn, 那么就能利用这些样本去估计这个分布的某些函数的期望值.

蒙特卡洛的思想就是用平均值来代替积分, 求期望

在粒子滤波中, 贝叶斯的后验概率计算要用到积分, 为了解决积分这个难的问题, 可以用蒙特卡洛采样来代替计算后验概率.

假设可以从后验概率中采取到N个样本粒子, 那么后验概率的计算公式可以表示为:



得到了后验概率, 需要得到当前状态的期望值

![exp_current_state](/home/yang/Desktop/github/blog/phd/exp_current_state.png)










































$$
p(x_{k}|y_{1:k-1})  = \int p(x_{k},x_{k-1}|y_{1:k-1})d_{x_{k-1}}\\ = \int p(x_{k}|x_{k-1},y_{1:k-1})p(x_{k-1}|y_{1:k-1})d_{x_{k-1}} \\= \int p(x_{k}|x_{k-1})p(x_{k-1}|y_{1:k-1})d_{x_{k-1}}
$$
















