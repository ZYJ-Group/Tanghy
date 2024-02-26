# 迁移学习策略的选择

## 模型性能评估

以下表格展示了不同模型配置下的性能指标，包括峰值信噪比（PSNR）、结构相似性指数（SSIM）、光谱角映射器（SAM）和平均绝对误差（MAE）：

| 配置         | PSNR   | SSIM   | SAM    | MAE     |
|------------|--------|--------|--------|---------|
| pretrain     | 5.1832 | 0.0050 | 31.5633| 136.4359|
| pretrain+train| 18.6516| 0.2045 | 2.6677 | 20.9044 |
| no pretrain + train | 17.4906| 0.1342 | 3.1822 | 26.3462 |

这些性能指标提供了对模型在不同配置下的表现的量化度量。

效果图：  
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/72861f00-8d23-478b-9320-9e47f64bf29b)  



## 小样本学习（Few-shot Learning）

[Few-shot Learning](https://github.com/learnables/learn2learn) 是一种特殊的机器学习设置，目标是让模型能够从非常少量的样本中快速学习新任务。如果小数据集非常有限，比如只有几个样本，那么任务可能会涉及到Few-shot Learning的策略。

## 领域适应（Domain Adaptation）

领域适应（Domain Adaptation）通常涉及到源域和目标域之间存在一些分布差异，目的是要调整模型以使其能够从源域泛化到目标域。如果大数据模型（源域）和小数据应用（目标域）之间存在一定的分布差异（比如不同的云层分布、不同的成像条件等），那么任务可以被视为领域适应问题。

### ADDA

ADDA 可以在 [这里](https://github.com/corenel/pytorch-adda) 找到。  

#### 实际测量结果

以下是通过实际实验得到的结果：

| 实验条件         | 平均损失 (Avg Loss) | 平均准确率 (Avg Accuracy) |
|-----------------|---------------------|--------------------------|
| Source only     | 2924.6131158644152  | 68.064517%               |
| Domain adaption | 93.3094972179782    | 12.741935%               |

#### 代码中的结果

以下是从提供的代码中得到的结果，用于参考对比：

| Source/Target                        | MNIST (Source) | USPS (Target)  |
|--------------------------------------|----------------|----------------|
| Source Encoder + Source Classifier   | 99.140000%     | 83.978495%     |
| Target Encoder + Source Classifier   | N/A            | 97.634409%     |

