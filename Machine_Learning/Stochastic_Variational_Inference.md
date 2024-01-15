# Stochastic Variance Inference

- 首先传统的VI是低效的，因为我们需要基于全部的数据集来更新local variable，然后基于更新后的local variable来更新global variable。当数据量变大后，参数更新就会耗费更多时间，SVI的作用就是将VI扩展到海量数据集上。


![](Pictures/Variational23.jpg)