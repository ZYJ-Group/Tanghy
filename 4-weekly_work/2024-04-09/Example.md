# 周报--04_03


## PPT制作  
  准备组会讲的ppt，将论文进行再一次的梳理，并将其中关于单时态去云部分的内容以及其中提出的不确定性量化相关的损失函数进行着重了解。  
  
### 不确定性量化  
#### 多元正态分布

考虑预测值 $\hat{y}_j$ 和实际值 $y_j$ ，我们假设预测误差遵循一个以 $\hat{y}_j$ 为均值、 $\Sigma$ 为协方差矩阵的K元正态分布。多元正态分布的概率密度函数（PDF）为：

$$
N(y_j|\hat{y}_j,\Sigma) = \frac{1}{\sqrt{(2\pi)^K |\Sigma|}} \exp\left(-\frac{1}{2}(y_j-\hat{y}_j)^T \Sigma^{-1} (y_j-\hat{y}_j)\right)
$$

其中， $\Sigma$ 是向量的维度， $|\Sigma|$ 是协方差矩阵 $\Sigma$ 的行列式。

#### 负对数似然损失

负对数似然损失是通过对上述概率密度函数取负对数得到的。对于单个观测，NLL损失为：

$$
\log(N(y_j|\hat{y}_j,\Sigma)) = \log\left(\frac{1}{\sqrt{(2\pi)^K |\Sigma|}}\right) - \frac{1}{2} (y_j-\hat{y}_j)^T \Sigma^{-1} (y_j-\hat{y}_j)
$$

$$
-\mathcal{L}_{NLL} (y_j|\hat{y}_j,\Sigma) = -\log\left(\frac{1}{\sqrt{(2\pi)^K |\Sigma|}}\right) + \frac{1}{2} (y_j-\hat{y}_j)^T \Sigma^{-1} (y_j-\hat{y}_j)
$$

将 $(2\pi)^K$ 项视为常数，可以简化为：

$$
\mathcal{L}_{NLL} (y_j|\hat{y}_j,\Sigma) = \frac{1}{2} \log((2\pi)^K |\Sigma|) + \frac{1}{2} (y_j-\hat{y}_j)^T \Sigma^{-1} (y_j-\hat{y}_j)
$$

对于整个数据集的所有像素，总的NLL损失是每个像素NLL损失的和：


$$
\mathcal{L}_{NLL} (\mathbf{Y}|\mathbf{\hat{Y}},\Sigma) \propto \sum \left( \log(|\Sigma_j|) + (y_j-\hat{y}_j)^T \Sigma_j^{-1} (y_j-\hat{y}_j) \right)
$$

## 实验测试
在探索Swin Transformer对不同损失函数的响应特性时，尤其是当应用于l2损失函数与基于不确定性量化的负对数似然（NLL）损失函数时，观察到了明显的性能差异。尽管Swin Transformer在采用l2损失时能够保持较为理想的性能表现，但是在应用不确定性量化的NLL损失时，其性能表现大幅下降。进一步的实验优化揭示了这一性能差异背后的原因：不确定性量化的NLL损失要求模型输出的前13个通道代表无云图像的预测平均值，而后续13个通道则需预测预测值的方差。这一额外约束对Swin Transformer这种参数量较大的模型产生了显著影响，导致其输出值在损失函数作用下不断缩小，并在模型的最后几层被强制正数化并限制在特定范围内，从而使模型性能受到最后一至两层的显著约束。  

鉴于此，当前的研究重点在于两个方向：首先是对Swin Transformer进行细致的修改，以提升其对不确定性量化NLL损失的适应性；其次是探索新的损失函数和模型设计，旨在寻找能够更有效地利用Swin Transformer结构优势的策略。通过这样的双轨并进策略，期望能够突破现有的性能瓶颈，为深度学习模型在复杂损失函数下的优化提供新的解决路径。  
