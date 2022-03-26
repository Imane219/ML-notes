# Gradient Descent

`梯度下降法`用来解决如下优化问题，求$\theta^*$
$$
\theta^* = \arg\min\limits_\theta L(\theta)
$$
$L$: Loss function  $\theta$:parameters



具体过程如下：

![](..\imgs\11.png)

## 学习率$\eta$

学习率决定了下降的步长，如果步长过大，有可能会跨过最低点，越优化损失函数越大；步长过小则下降速率很慢。因此一个简单的做法是**让$\eta$随着走的步数(时间)变小**：$\eta^t = \frac{\eta}{\sqrt{t+1}}$. 一开始距离最低点较远，可以步长大一些；当离最低点越来越近则需要更加谨慎。

### Adagrad

对每个参数采用不同的学习率，对于参数$w$而言，其值的更新如下：
$$
w^{t+1} = w^t - \frac{\eta^t}{\sigma^t}g^t\\
\eta^t = \frac{\eta}{\sqrt{t+1}}, g^t=\frac{\partial L(\theta^t)}{\partial w}, \sigma^t=\sqrt{\frac{1}{t+1}\sum\limits^t_{i=0}(g^i)^2}
$$
其中，$\eta^t$是随时间更新的学习率，$g^t$是第$t$次更新的微分值，$\sigma^t$是前$t$次的微分值的**root mean square**.化简后结果如下：
$$
w^{t+1} = w^t - \frac{\eta}{\sqrt{\sum^t_{i=0}(g^i)^2}}g^t
$$
理解如下：以二次式为例，一个最好的步长是一步直接跨到最低点，此时步长值为：**一次微分/二次微分**。但是二次微分计算量比较大，采用一次微分平方再开根的方式来模拟二次微分值。

![](..\imgs\12.png)

![](..\imgs\13.png)

## 随机梯度下降(Stochastic Gradient Descent)