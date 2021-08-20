#### 进入neat

Hello, teacher. Hello, everyone. I re implemented the project according to the neat algorithm. Before I talk about the project, let me give a brief introduction to the neat algorithm.

老师好，大家好。我根据neat算法重新实现了这个项目。在我谈论项目之前，让我先对neat算法做一个简单的介绍。

His full name is neuroevolution of augmenting topologies, which is a genetic algorithm (GA) for the generation of evolving artificial neural networks.

他的全称为...,是一种...遗传算法

In short, this algorithm generates many individuals to play the game, let them compete, evaluate each individual through fitness, eliminate bad individuals, select good individuals to reproduce to obtain better kids, and explore more possibilities through mutation. Here, reproduction is called crossover.

简单来说，这个算法通过生成很多个体去玩游戏，让他们竞争，通过fitness评价各个个体，淘汰差的个体，让好的个体繁衍后代，同时进行变异来探索更多可能。在这里，繁殖被称为交叉

#### 结合神经网络

Interestingly, neat combines genetic algorithm and neural network. Here, each individual corresponds to one neural network, which is called a genome.

有趣的是，neat结合了遗传算法和神经网络。在这里，每一个个体对应一个神经网络，这被叫做基因组.

This figure shows how a neural network can be represented by a genome. The node gene is the definition of each node in the neural network. It indicates the node type. An input, output or hidden node. The connection gene represents the connection information between the nodes, including the associated node, weight, whether the connection is enabled, and the proprietary innovation ID, which is used to distinguish different connections.

这幅图显示了神经网络是如何用基因组来表示的。节点基因是神经网络中每个节点的定义。它指示节点类型。输入、输出或隐藏节点。连接基因表示节点之间的连接信息，包括关联节点、权重、连接是否启用以及专有创新ID, which用于区分不同的连接

#### 变异

There are two ways of mutation, adding node or adding connection.

两种方式变异

It should be noted that when adding a node, the node will cut off the connection between other two nodes, which will be disabled. So you see one more disabled record added here.

需要注意的是，当添加一个节点时，该节点会切断其他两个节点之间的连接，这将被禁用。 所以你会看到这里又添加了一个禁用的记录。 

In addition, the weight value of genes in each generation may also change in a certain range

此外，每一代基因的权重值也可能在一定范围内发生变化 

#### 繁殖/交叉

As for the reproduction of excellent individuals, this process is called genome crossover, as I just mentioned earlier. Here, genes are aligned by innovation ID. If two genes at the same location are different, one gene is randomly selected for inheritance

至于优秀个体的繁殖，这个过程被称为是基因组的交叉，就如我刚才提到那样。在这里，基因通过创新id对齐。如果同一位置双方基因不同，随机选择一方的基因继承

The reason why disjoint and excess genes are marked on the graph is that they are used to calculate the degree of difference between populations

不相交基因和多余基因在图上标记的原因是它们被用来计算群体之间的差异程度

If the gene gap between some birds and others is greater than the threshold, these birds will be considered as new species. Neat algorithm will protect new species and let them compete within species. When new species grow to a **certain extent**, they will participate in the competition among species.

如果有一些鸟基因与其他鸟差距大于阈值，则这些鸟将被认为属于新的物种。neat算法将会保护新物种，让其物种内部竞争，当新物种壮大再参与物种间的竞争。

I won't **elaborate** here 

这里我就不详细说了

#### 回到项目 apply

So now back to our project, the neat algorithm will play the game round after round until it selects good enough birds or reaches the maximum number of generations we set 

那么现在回到我们的项目，neat算法会一轮又一轮地玩游戏，直到它选出足够优秀的鸟或者达到我们设定的最大繁衍代数量

First, I need to define the original form of neural network. The input layer is the eye of the agent, and the information in it is actually what the agent can see.

首先，我需要定义神经网络的原始形式。 输入层是agent的眼睛，里面的信息其实就是agent可以看到的。 

Now let's look at the pictures of the game. We need to find the input of the neural network. We know that the qlearing project selects these two distances as the input information obtained by the agent in the environment. This is due to the limitation of qtable size. In other words, it cannot obtain more, otherwise the number of states of qtable will be too large. But the neat project does not have this limitation. So I chose these as input information

现在让我们看看游戏的图片。我们要找到神经网络的输入。我们知道，the qlearning project选择了这两个距离作为agent在环境中获取的信息。这是因为qtable大小的限制。也就是说不能选择更多的信息输入，否则qtable的状态数会非常大。但是neat项目没有这个限制。所以我选择了这些输入信息

....

...输入结点

...

For the output node, the output value needs to be used to judge whether to jump. I use the tanh function to map the output value to the interval (- 1,1). If the result is greater than 0.5, the bird will jump

对于输出节点，需要根据输出值来判断是否跳转。 我使用 tanh 函数将输出值映射到区间 (- 1,1)。 如果结果大于0.5，小鸟会跳 



#### apply 2

Then the structure of the neural network may change. At last the algorithm will select the best network, that is, the best bird.

然后神经网络的结构可能会发生改变，最后算法将挑选出最好的网络，也就是选出最好的鸟



#### game

Regarding the game itself, I have made major changes on the basis of the original game. The original game author did not create birds, tubes, and floors. I created them. In order to manage a flock of birds, adjust the number of tubes and how they appear, so I can increase the difficulty and challenge more easily. 

关于游戏本身，我在原来游戏的基础上做了较大的改动。原来的游戏作者并没有创造鸟，管，地板这些类，我创造了，为了管理一群鸟，调整管子数量和他们如何出现，所以我更轻松能增加难度，挑战性