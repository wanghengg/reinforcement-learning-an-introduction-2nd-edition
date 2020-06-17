# Elements of reinforcement learning

* 强化学习四个要素：a plolicy, a reward signal, a value function, a model of the environment

    A policy defines the learning agent’s way of behaving at given time. 策略(policy)就是从感知到的环境状态到处于这种状态时所要采取的措施的映射。

    A reward signal defines the goal of a reinforcement learning problem.在每个时间步，环境都会都会给agent发送一个奖励(reward)，智能体(agent)的唯一目的就是在长期内获得最大的累计奖励。奖励信号是调整策略的首要条件。如果在某一策略下的行动的奖励值比较低，那么下次遇到相同的情况时会更改策略选择别的动作。

    奖励信号在即时意义上反映了策略的好坏，而价值函数从反映了长时间的策略选择好坏情况。The value of a state is the total amount of reward an agent can expect to accumulate over the future, starting from that state.(从当前状态期望的未来奖励的累加。)Action choices are made based on value judgments. We seek actions that bring about states of highest value, not highest reward, because these actions obtain the greatest amount of reward for us over the long run.动作的选择基于价值函数的值，我们要寻找的是能够产生highest value而不是highest reward的动作，因为这样的动作能够在长期内带来最大的回报。但是，reward直接由环境给出，容易计算，而value取决于从当前状态一直到生命周期结束所有的状态奖励，很难计算。实际上，强化学习的最重要的部分就是寻找最大累计回报的方法。

    A model of environment就是模仿环境的行为， 具体来说就是推断出环境的行为方式。

## Limitations and Scope

* think of the state as whatever information is available to the agent about its environment.