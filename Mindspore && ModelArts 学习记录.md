# Mindspore && ModelArts 学习记录

由于我的目标是要迁移pytorch代码，所以和pytorch同步学习，并且会进行一些比较。

## Mindspore安装

> Mindspore 可以在ModelArts使用，也可以在本地使用,虽然ModelArts 计算资源免费不过上传方式确实太复杂了，所以学习阶段也有必要安装一下，我装在实验室服务器上，环境为Ubuntu18.04

MindSpore安装指南: https://www.mindspore.cn/install#installTip

官方推荐在已经有安装部分环境时使用手动安装，如果你的电脑之前没有配过环境建议直接用给的脚本自动安装。我这里只列出我的步骤

```bash
#创建conda环境：
conda create -c conda-forge -n mindspore_py38 python=3.8 -y
conda activate mindspore_py38

#在 mindspore_py38中安装mindspore
conda install mindspore-gpu cudatoolkit=11.1 -c mindspore -c conda-forge

#添加nvcc的安装路径添加到PATH与LD_LIBRARY_PATH环境变量中，当然之前安装了其他CUDA版本或者CUDA安装路径不同要替换成你的
export PATH=/usr/local/cuda-11.1/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-11.1/lib64:$LD_LIBRARY_PATH

#检查version
python -c "import mindspore;mindspore.run_check()"
```

## 手写数字识别demo

下载并处理MNIST数据集

```python
from mindvision.dataset import Mnist

download_train = Mnist(path="./mnist", split="train", batch_size=32, repeat_num=1, shuffle=True, resize=32, download=True)

download_eval = Mnist(path="./mnist", split="test", batch_size=32, resize=32, download=True)

dataset_train = download_train.run()
dataset_eval = download_eval.run()
```

训练

```python
from mindvision.dataset import Mnist
from mindvision.classification.models import lenet  #引入vision中的LeNet网络模型
import mindspore.nn as nn  #神经网络Cell
from mindspore.train import Model
from mindspore.train.callback import ModelCheckpoint, CheckpointConfig
from mindvision.engine.callback import LossMonitor


download_train = Mnist(path="../data/mnist", split="train", batch_size=32, repeat_num=1, shuffle=True, resize=32)
download_eval = Mnist(path="../data/mnist", split="test", batch_size=32, resize=32)

dataset_train = download_train.run()
dataset_eval = download_eval.run()

network = lenet(num_classes=10, pretrained=False)


# 定义损失函数,交叉熵损失函数
net_loss = nn.SoftmaxCrossEntropyWithLogits(sparse=True, reduction='mean')

# 定义优化器函数,Momentum
net_opt = nn.Momentum(network.trainable_params(), learning_rate=0.01, momentum=0.9)


# 设置模型保存参数
config_ck = CheckpointConfig(save_checkpoint_steps=1875, keep_checkpoint_max=10)

# 应用模型保存参数
ckpoint = ModelCheckpoint(prefix="lenet", directory="./learnPython/mindspore/learn/handwrittenDigitRec/lenet", config=config_ck)

# 初始化模型参数
model = Model(network, loss_fn=net_loss, optimizer=net_opt, metrics={'accuracy'})

# 训练网络模型
model.train(10, dataset_train, callbacks=[ckpoint, LossMonitor(0.01, 1875)])


acc = model.eval(dataset_eval)

print("{}".format(acc))
```

测试

```python
#加载测试
from mindvision.dataset import Mnist
from mindvision.classification.models import lenet  #引入vision中的LeNet网络模型
from mindspore import load_checkpoint, load_param_into_net
import numpy as np
from mindspore import Tensor
import mindspore.nn as nn  #神经网络Cell
import matplotlib.pyplot as plt
from mindspore.train import Model


network = lenet(num_classes=10, pretrained=False)


# 加载已经保存的用于测试的模型
param_dict = load_checkpoint("./lenet/lenet-1_1875.ckpt")
# 加载参数到网络中
load_param_into_net(network, param_dict)

# 定义损失函数,交叉熵损失函数
net_loss = nn.SoftmaxCrossEntropyWithLogits(sparse=True, reduction='mean')
# 定义优化器函数,Momentum
net_opt = nn.Momentum(network.trainable_params(), learning_rate=0.01, momentum=0.9)
# 初始化模型参数
model = Model(network, loss_fn=net_loss, optimizer=net_opt, metrics={'accuracy'})

mnist = Mnist("~/data/mnist", split="train", batch_size=6, resize=32)
dataset_infer = mnist.run()
ds_test = dataset_infer.create_dict_iterator()
data = next(ds_test)
images = data["image"].asnumpy()
labels = data["label"].asnumpy()

plt.figure()
for i in range(1, 7):
    plt.subplot(2, 3, i)
    plt.imshow(images[i-1][0], interpolation="None", cmap="gray")
plt.show()

# 使用函数model.predict预测image对应分类
output = model.predict(Tensor(data['image']))
predicted = np.argmax(output.asnumpy(), axis=1)

# 输出预测分类与实际分类
print(f'Predicted: "{predicted}", Actual: "{labels}"')

```

效果：![image.png](https://s2.loli.net/2022/05/16/SN6ezYF49gTLI8B.png)

## 参考

MindSpore Docs: https://www.mindspore.cn/docs/zh-CN/r1.7/index.html