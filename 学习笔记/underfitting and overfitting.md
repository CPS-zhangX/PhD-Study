### 欠拟合和过拟合

对于深度学习或机器学习模型而言，我们不仅要求它对训练数据集有很好的拟合（训练误差），同时也希望它可以对未知数据集（测试集）有很好的拟合结果（泛化能力），所产生的测试误差被称为泛化误差。

**度量泛化能力的好坏**，最直观的表现就是模型的过拟合（overfitting）和欠拟合（underfitting）。过拟合和欠拟合是用于描述模型在训练过程中的两种状态。一般来说，训练过程会是如下所示的一个曲线图

![image](https://raw.githubusercontent.com/CPS-zhangX/PhD-Study/master/images/fitting.jpg)

训练刚开始的时候，模型还在学习过程中，处于欠拟合区域。随着训练的进行，训练误差和泛化误差都下降。在到达一个临界点之后，训练集的误差（训练误差）下降，测试集的误差（泛化误差）上升了，
这个时候就进入了过拟合区域——由于训练出来的网络**过度拟合了训练集**，对训练集以外的数据却不work。

### 欠拟合
模型复杂度低，模型在训练集上就表现很差，**没法学习到数据背后的规律**。欠拟合基本上都会发生在训练刚开始的时候，经过不断训练之后欠拟合应该不怎么考虑了。但是如果真的还是存在的话，可以通过**增加网络复
杂度**或者在**模型中增加特征**，这些都是很好解决欠拟合的方法。

### 过拟合
过拟合是指训练误差和测试误差之间的差距太大。换句换说，就是模型复杂度**高于**实际问题，模型在训练集上表现很好，但在测试集上却表现很差。模型对训练集**"死记硬背"**（记住了不适用于测试集的训练集性质或特点），
没有理解数据背后的规律，**泛化能力差**。

![image](https://raw.githubusercontent.com/CPS-zhangX/PhD-Study/master/images/fitting2.jpg)
```diff
- 论文中说明没有overfitting的方法：画张折线图：x轴是你的树的数量（或其它参数），y轴是在validation上的结果（１０份平均）。这图显示你用的树的数量正好对应y的一个局部最大值处即可。
```

造成overfitting的原因：

1. **训练数据集样本单一，样本不足**。如果训练样本只有负样本，然后那生成的模型去预测正样本，这肯定预测不准。所以训练样本要尽可能的全面，覆盖所有的数据类型。 

2. **训练数据中噪声干扰过大**。噪声指训练数据中的干扰数据，存在错误或异常（偏离期望）。过多的干扰会导致记录了很多噪声特征，忽略了真实输入和输出之间的关系。

3. **模型过于复杂**。模型太复杂，已经能够“死记硬背”记下了训练数据的信息，但是遇到没有见过的数据的时候不能够变通，泛化能力太差。我们希望模型对不同的模型都有稳定的输出。
模型太复杂是过拟合的重要因素。

### 如何解决overfitting
**核心**：显著减少测试误差，而不过度增加训练误差，从而提升模型的泛化能力！**下面的所有方法都是正则化的一种**。

1. **数据集增强data augmentation**：获取和使用更多的数据，这是根本性方法。实际中我们拥有的数据集是有限的。解决这个问题的一种方法就是**创建“假数据”**并添加到训练集中。我们以图像数据集举例，
能够做：旋转图像、缩放图像、随机裁剪、加入随机噪声、平移、镜像等方式来增加数据量。

2. **采用合适的模型simpler model structure**，也就是控制模型的复杂度！通过实验和竞赛发现，对于CNN来说，层数越多效果越好，但是也更容易产生过拟合，并且计算所耗费的时间也越长。
**奥卡姆剃刀法则**：选择简单、合适的模型解决复杂的问题。

3. **降低特征的数量**：可以考虑降低特征的数量，也就是人工选择保留哪些特征。

4. **L1正则化regularization**：在原始的损失函数后面加上一个L1正则化项，即全部权重w的绝对值的和，再乘以$\frac{\lambda}{n}$，其中$\lambda$是可调的参数。则损失函数变为：
$$ C = C_0 + \frac{\lambda}{n}\sum_i |w_i| $$
对应的导数为：![image](https://raw.githubusercontent.com/CPS-zhangX/PhD-Study/master/images/l1.jpg)

那么权重更新为：![image](https://raw.githubusercontent.com/CPS-zhangX/PhD-Study/master/images/l12.jpg)

当w=0时，相当于使用未经正则化的方法去更新w；w>0时，sgn(w)>0，则梯度下降时更新后的w变小；w<0时，sgn(w)<0，则w变大。总之，L1会使得w的值往0去靠近，**这也是L1会产生更 稀疏的解**的原因。网络中的权重尽可能为0，这意味着**减小了网络复杂度，防止了overfitting**。

5. **L2正则化regularization**：又名weight decay。原始的损失函数后面再加上一个L2正则化项，即全部权重w的平方和，再乘以$\frac{\lambda}{2n}$。损失函数变为：
$$C = C_0 + \frac{\lambda}{2n}\sum_i |w^2_i|$$
对应的导数为(对b没有影响)：![image](https://raw.githubusercontent.com/CPS-zhangX/PhD-Study/master/images/l2.jpg)

那么权重更新为：![image](https://raw.githubusercontent.com/CPS-zhangX/PhD-Study/master/images/l22.jpg)

由于$n,\lambda,\eta$都大于0，所以$1-\frac{\eta \lambda}{n}$小于1。那么w将逐渐减小并趋紧0。这就是名字“weight decay”的由来。更小的权重参数 [公式] 意味着模型的复杂度更低，对训练数据的拟合刚刚好，不会过分拟合训练数据，从而提高模型的泛化能力。



6. **Dropout**：Dropout 指的是在训练过程中**每次按一定的概率（比如50%）随机地“删除”一部分隐藏单元（神经元）**。所谓的“删除”不是真正意义上的删除，其实就是将该部分神经元的激活函数设为0（激活函数的输出为0），让这些神经元不计算而已。

![image](https://raw.githubusercontent.com/CPS-zhangX/PhD-Study/master/images/dropout.jpg)

对overfitting有效的原因在于两点：**一是这相当于在训练的过程中使用了不同的训练模型，那么最终的训练结果就是不同模型的平均输出；另一方面是降低了网络对单个神经元的依赖，提升泛化能力**。

7. **Early stopping**：模型的训练过程就是对模型参数进行学习更新的过程，这个过程往往会用到一些迭代方法。Early stopping是一种迭代次数截断的方法来防止过拟合的方法，即在模型对训练数据集迭代收敛之前停止迭代来防止过拟合。

为了获得性能良好的神经网络，训练过程中可能会经过很多次epoch（遍历整个数据集的次数，一次为一个epoch）。如果epoch数量太少，网络有可能发生欠拟合；如果epoch数量太多，则有可能发生过拟合。Early stopping旨在解决epoch数量需要手动设置的问题。具体做法：**每个epoch（或每N个epoch）结束后，在验证集上获取测试结果，随着epoch的增加，如果在验证集上发现测试误差上升，则停止训练，将停止之后的权重作为网络的最终参数。**缺点是无法保证损失函数足够小。

8. **Bagging and random forest**: 就是 通过**集成学习**的思路进行正则化，使用k个相互独立的DNN网络，首先我们要对原始的m个训练样本进行有放回随机采样，构建N组m个样本的数据集，然后分别用这N组数据集去训练我们的DNN。即采用我们的前向传播算法和反向传播算法得到N个DNN模型的W,b参数组合，最后对N个DNN模型的输出用加权平均法或者投票法决定最终输出。问题在于参数变为原来的k倍。

**详见学习笔记中的"集成学习"一文。**

9. **交叉验证**：详见“交叉验证”一文

- [1] [欠拟合、过拟合及如何防止过拟合](https://zhuanlan.zhihu.com/p/72038532)

- [2] [深度神经网络（DNN）的正则化](https://www.cnblogs.com/pinard/p/6472666.html)

- [3] [机器学习防止欠拟合、过拟合方法](https://zhuanlan.zhihu.com/p/29707029)
