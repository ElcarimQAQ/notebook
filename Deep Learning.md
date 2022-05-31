监督学习（Supervised Learning）

无监督学习（Unsupervised Learning）

给定机器函数寻找的范围

强化学习（Reinforcement Learning）



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
