参考吴恩达&&西瓜书

## 绪论



### 基础术语

| 名词                                                       | 含义                                 |
| :--------------------------------------------------------- | ------------------------------------ |
| data set（数据集）                                         | 一批数据记录的集合                   |
| instance（示例）/sample（样本）/feature vector（特征向量） | 每条记录中关于一个事件或对象的描述   |
| attribute（属性）/feature（特征）                          | 反应事件或对象的表现或性质           |
| attribute value                                            | 属性上的取值，如西瓜的颜色"青黑"     |
| dimensionality（维数）                                     | 每个示例的属性描述个数classification |
| classification（分类）                                     | 预测的是离散值的任务                 |
| regression（回归）                                         | 预测的是连续值的任务                 |
| generalization（泛化）                                     | 学的模型适用于新样本的能力           |

### 归纳偏好

一个数据集训练出了不同的模型，如何选择模型。

奥卡姆剃刀：选择最简单的那个

但是仍有不适用的情况，对于任何一个学习算法$a$，若在某些问题上比$b$好，必然存在一些问题$b$比$a$好。

证明：

![image-20220319213047959](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220319213047959.png)

## 模型评估与选择

### 经验误差与过拟合

m个样本中有a个分类错误

error rate : $E=\frac{a}{m}$

accuracy:$1-\frac{a}{m}$

学习器在训练集上的误差称为training error（训练误差），在新样本上的误差称为generalization error（泛化误差）

**过拟合（overfittting）**：学习器把训练样本学的太好，以至于泛化性能下降

![image-20220320201218783](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220320201218783.png)

### 评估方法

测试集：测试学习器对样本的判别能力
测试集尽可能与训练集互斥

划分测试集/训练集

留出法：直接将数据集划为两个互斥的合集

交叉验证法

自助法

## Regression

目标：预测宝可梦净化后的cp值

![ ](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220308204106033.png)



![image-20220308205303781](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220308205303781.png)

上标用来代指完整的个体。

w：weight

b：bias

 $L$ ：某函数有多不好,衡量一组b和w的好坏，此处使用 的是估测误差

![image-20220308211106033](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220308211106033.png)



挑选best fucntion：遍历w，b让L最小

![image-20220308211753367](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220308211753367.png)

用梯度下降（Gradient Desent）解上面这个函数

### Gradient Desent(梯度下降)

目标：找一个最好的function

遍历是没有效率的，可以随机选取一个初始点，根据微分选择合适的方向，w的梯度下降：

 ![image-20220308212438980](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220308212438980.png)

如果有多个参数，并没有太大区别

![image-20220308212756665](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220308212756665.png)

 ![image-20220308213248865](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220308213248865.png)

更复杂的model：多项式回归



#### 调学习率

![image-20220309212046928](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220309212046928.png)

  ![image-20220309212753038](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220309212753038.png)

  ![image-20220309222207988](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220309222207988.png)

**过拟合（Overfitting）**：

![image-20220308214317375](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220308214317375.png)

### Regularization(正则化)

 期望w更小，来让输入不敏感，在Loss function中加入一部分:

![image-20220308215539483](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220308215539483.png)



error 可能来自于bias和variance

![image-20220309204837249](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220309204837249.png)



![image-20220309205034443](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220309205034443.png)

![image-20220309205553160](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220309205553160.png)

分测试集和验证集：

![image-20220309210935682](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220309210935682.png)

## 强化学习

**强化学习**（Reinforcement Learning，简称**RL**）是机器学习的一个重要分支，在强化学习中，包含两种基本的元素：**状态**与**动作**，**在某个状态下执行某种动作，这便是一种策略**，学习器要做的就是通过不断地探索学习，从而获得一个好的策略。例如：在围棋中，一种落棋的局面就是一种状态，若能知道每种局面下的最优落子动作，那就攻无不克/百战不殆了

若将状态看作为属性，动作看作为标记，易知：**监督学习和强化学习都是在试图寻找一个映射，从已知属性/状态推断出标记/动作**，这样强化学习中的策略相当于监督学习中的分类/回归器。但在实际问题中，**强化学习并没有监督学习那样的标记信息**，通常都是在**尝试动作后才能获得结果**，因此强化学习是通过反馈的结果信息不断调整之前的策略，从而算法能够学习到：在什么样的状态下选择什么样的动作可以获得最好的结果。

### 任务和奖赏
​	RL 通常使用**马尔科夫决策过程（Markov Decision Process ）**：机器处在一个环境中，每个状态为机器对当前环境的感知；机器只能通过动作来影响环境，当机器执行一个动作后，会使得环境按某种概率转移到另一个状态；同时，环境会根据潜在的奖赏函数反馈给机器一个奖赏。综合而言，强化学习主要包含四个要素：状态、动作、转移概率以及奖赏函数。

![image-20220323223441843](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20220323223441843.png)

- 环境E

- 状态空间X：机器对环境的感知，所有可能的状态称为状态空间

- 动作空间A：机器对环境的感知，所有可能的状态称为状态空间

- 转移函数P：机器对环境的感知，所有可能的状态称为状态空间

- 奖赏R：机器对环境的感知，所有可能的状态称为状态空间

  <img src="https://cdn.kesci.com/upload/image/q623dlbo1n.png?imageView2/0/w/960/h/960" alt="Image Name"  />

  

策略π：根据这个策略便能知道在什么状态下应该执行什么动作

- 确定性策略：π（x）=a，即在状态x下执行a动作；
- 随机性策略：P=π（x,a），即在状态x下执行a动作的概率。

目的：找到使长期累计奖赏最大化的策略
