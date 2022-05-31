平面目标跟踪的目标是从模板图像T的$i_{th}$输入帧$I_i\in \mathbb{R}^{n\times n} $恢复**underlying homography transformation**，$I_i $ is $n \times n$.

![image.png](https://s2.loli.net/2022/05/30/hOV12WZHlD5nJk4.png)

$p$:$(u,v,1)^T$ 像素的齐次坐标（ homogenous coordinates）向量，$I(p)$像素

$P$:四角坐标矩阵，3*4

$H_i $: transformation矩阵

$P_T$: T坐标矩阵