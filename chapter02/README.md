# Note

## A K-armed Bandit Problem

每次有$k$个不同的选择，每次选择之后有一个$reward$，目标是在一个时间周期内使得$expected total reward$最大。在$k$臂赌博机问题里面，用$A_t$表示在时间步$t$选择的动作，用$R_t$表示相应的奖励。所以任意的动作$a$对应的期望奖励为：
$$
q_*(a) \doteq{\Epsilon[R_t|A_t=a]}
$$
用在时间步$t$对动作$a$估计的值为$Q_t(a)$，我们希望$Q_t(a)$接近$q_*(a)$

在每个时间步至少有一个动作的***expected value***是最大的，把这些动作叫做***greedy actions***，当选择这些动作中的一个时，称为***exploit your current knowledge of the values of the actions***。如果选择***non-greedy action***，称为***exploring***，***exploitation***可以在当前步最大化***expected value***，但是***exploration***在长期内可能得到***greater total reward***.

如果还有足够的***steps***，不确定是否有其他的动作与**greedy actions**一样好，此时可以进行**exploration**，短时间内可能**reward**比较小，但是一旦找到了更好的动作(**better action**)，那么接下来可以多次利用它们，使得长期的累计奖励(**long run cumulative reward**)更高。

***The need to balance exploitation and exploration is a distinctive challenge that arises in reinforcement learning.***

## Action-value Methods

***True value of an action is the mean reward when that action is selected***，计算每个动作的value的一种自然的方法是：
$$
Q_{t}(a) \doteq \frac{\text { sum of rewards when } a \text { taken prior to } t}{\text { number of times } a \text { taken prior to } t}=\frac{\sum_{i=1}^{t-1} R_{i} \cdot \mathbb{1}_{A_{i}=a}}{\sum_{i=1}^{t-1} \mathbb{1}_{A_{i}=a}}
$$
其中$\mathbb{1}_{predicate}$是一个随机变量，当$predicate$为**true**时，$\mathbb{1}_{predicate}$为1，当$predicate$为**false**时，$\mathbb{1}_{predicate}$为0。如果分母为0，那么定义$Q_t(a)$为某个默认值，例如0。当分母趋近于无穷大时，那么$Q_t(a)$收敛于$q_*(a)$。

最简单动作选择策略就是选择有*highest expected value*的动作，也就是*greedy action*，如果同时有超过一个*greedy action*，那么从这些*greedy action*中任意选择一个，将***greedy action selection method***定义为：
$$
A_t \doteq \arg \max _{a} Q_{t}{a}
$$
为了不每次都使用*greedy action selection*，可以定义一个概率$\varepsilon$，每次以概率$\varepsilon$从所有动作中随机选择一个(**exploration**)，讲这种方法叫做$\mathbf{\mathit{\varepsilon -greedy\space methods} } $

## The 10-armed Testbed

<img src="https://gitee.com/wanghengg/picture/raw/master/2020/image-20200624183724050.png" alt="image-20200624183724050" style="zoom: 67%;" />

**Greedy method**的长期表现远比$\mathbf{\mathit{\varepsilon-greedy \space method}}$效果差的原因是，**greedy method**容易陷入**suboptimal actions**。很多动作因为初始采样的时候reward很小(因为reward服从正态分布，初次采样时可能刚好采样到比较小的reward)，所以后面的动作选择就忽略了这些动作，导致这些动作以后再也没有被选择过，实际上这些动作的效果可能比当前的greedy action更好。

$\mathbf{\mathit{\varepsilon-greedy \space method}}$相对于$greedy \space method$的优势取决于任务的不同。如果**reward**的方差比较大，则需要的更多的**exploration**去寻找最优解，$\mathbf{\mathit{\varepsilon-greedy \space method}}$相对于$greedy \space method$的优势更加明显。另一方面，如果**reward**的方差为0，那么每个动作只需要一次尝试就能知道对应的动作值(value of the action)。这种情况下不需要*exploration*，$greedy \space method$就是最好的方法。在其他情况下，比如任务是非静态的(the true value of the actions changes over time)，此时需要*exploration*来确定是否有其他的动作变得比*greedy action*更好。

# Exercise

## exercise 2.1

> In $\varepsilon$-greedy action selection, for the case of two actions and $\varepsilon=0.5$, what is the probability that the greedy action is selected?

此例中一共有两种可选择的动作，一种选择时greedy action，另一种是explorative action，同时每次动作之前随机选择动作的概率是$\varepsilon=0.5$，所以选择explorative action的概率是$0.5 * 0.5 = 0.25$，因此选择greedy action的概率是$1-0.25=0.75$。

## exercise 2.2	Bandit example

> Consider a $k$-armed bandit problem with $k$ = 4 actions, denoted 1, 2, 3 and 4. Consider applying to this problem a bandit algorithm using $\varepsilon$-greedy action selection, sample-average action-value estimates, and initial estimates of $Q_1(a)=0$, for all $a.$ Suppose the initial sequence of actions and rewards is $A_1=1, R_1=1, A_2 = 2, R_2 = 1, A_3 = 2, R_3 = 2, A_4 = 2$, $R_4 = 2, A_5 = 3, R_5 = 0.$ On some of these time steps the $\varepsilon$ case may have occurred, causing an action to be selected at random. On which time steps did this definitely occur? On which time steps could this possibly have occurred? 

$A_2$ and $A_5$ were definitely exploratory. Any of the others could have been exploratory.

## exercise 2.3

> In the comparison shown in Figure 2.2, which method will perform best in the long run in terms of cumulative reward and probability of selecting the best action? How much better will it be? Express your answer quantitatively.



