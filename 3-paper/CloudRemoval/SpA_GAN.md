# 去云文献阅读-1/3（大方向/篇数）
# Cloud Removal for Remote Sensing Imagery vai Spatial Attention Generative Adversarial Network（标题/关键词）
- Pan Heng（作者）
- 链接：[paper](https://arxiv.org/abs/2009.13015)
- 阅读时间：2023/12/04

## 简介
    光学遥感图像由于其高分辨率和稳定的几何特性，在许多领域得到了广泛的应用。然而，遥感影像不可避免地受到气候的影响，尤其是云的影响。去除高分辨率遥感卫星影像中的云是对其进行分析前必不可少的预处理步骤。出于大规模训练数据的考虑，神经网络在许多图像处理任务中取得了成功，但利用神经网络去除遥感影像中云的研究还比较少。我们采用生成对抗网络来解决这一任务，并将空间注意力机制引入到遥感图像去云任务中，提出了一种名为空间注意力生成对抗网络( SpA GAN )的模型，该模型模仿人类视觉机制，通过局部到全局的空间注意力对云区域进行识别和聚焦，从而增强这些区域的信息恢复，生成质量更好的无云图像。在与现有去云模型(条件GAN ,循环GAN)在开源RICE数据集上的对比实验中，SpA GAN在峰值信噪比( PSNR )和结构相似度( SSIM )两个指标上都取得了最好的性能。证明了空间注意力机制对于提高去云图像质量的有效性以及模型在去云任务上的优越性能。Sp GAN的代码为https://github.com/Penn000/SpAGAN_for_cloud_removal.

## 关键词
    高分辨率遥感影像、云去除、生成对抗网络、空间注意力。

## 实验方法
**Generator--SPANet（空间注意力网络）**  
    ![SPANet](https://github.com/ZYJ-Group/Tanghy/assets/94824386/f283d62d-ef30-4aed-822e-3096e15de0d9)  
     Sp A Gan的生成器( a )。它采用3个标准残差块提取特征，4个空间注意块( SAB ) ( b )分4个阶段逐步识别云，2个残差块重建干净的背景。一个SAB包含3个空间注意力残差块( SARBs ) ( c )和1个空间注意力模块( SAM ) ( d )。  

**Discriminator--普通的卷积神经网络**  
     ![dis](https://github.com/ZYJ-Group/Tanghy/assets/94824386/704d982d-2899-4809-868e-c3d71ac0b93c)  

**Loss**  
    1. SpA GAN的总损失为：  
    ![loss_spagan](https://github.com/ZYJ-Group/Tanghy/assets/94824386/33cbd7aa-478e-4c9b-96ca-d4b802d9638a)  
    2. 条件GAN的损失函数：  
    ![loss_cgan](https://github.com/ZYJ-Group/Tanghy/assets/94824386/ac090c36-a539-4e46-b022-9ce4f925382d)  
    3. 标准l1损失函数：  
    ![loss_l1](https://github.com/ZYJ-Group/Tanghy/assets/94824386/f33b1faa-7eda-4198-839d-95694341ea84)  
    4. 注意力损失函数：  
    ![loss_att](https://github.com/ZYJ-Group/Tanghy/assets/94824386/f064c4f0-2b6f-4b16-9f6b-60d7897316c8)  

## 实验  
**数据集**  
    Remote sensing Image Cloud rEmoving (RICE)，RICE数据集由RICE1和RICE2两个子集合组成，可在[链接](https://github.com/BUPTLdy/RICE_DATASET)上获取。  

**评估指标**  
    1. PSNR  
    峰值信噪比( PSNR )是评价图像质量最广泛、最常用的客观指标，其计算公式为：  
    ![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/1c5ac4de-45fd-4296-b3a5-f99298a7e6ae)  
    其中n是像素值的位数，对于灰度图像，n为8。MSE是图像X和Y之间的均方误差，计算为：
    ![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/742dfdee-49cc-4d86-bf26-3cc292398ae0)  
    PSNR值一般在20 ~ 40之间，其值越大，表示预测图像与真实图像的距离越近，预测质量越好。  

    2. SSIM
    SSIM是一种通过亮度、对比度、结构三个方面来衡量两幅图像相似性的评价方法，其公式分别为：
    ![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/1db07b68-4eab-492e-8ef3-47ec30e93dbf)  
    在这里，C1，C2，C3为避免除零误差而取常数，μ σ为图像的均值和方差，XY σ为图像X和Y的协方差。因此，SSIM的公式为：  
    ![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/d94a2a83-8eca-4d3d-b2ac-3c7000ae16de)  
    SSIM的取值范围在0 ~ 1之间，取值越大表示两幅图像越相似。如果取值为1，则两幅图像完全相同。  

**实验设置**  
    对于RICE数据集，在RICE1中选择400张图像进行训练，100张图像进行测试，在RICE2中选择588张图像进行训练，148张图像进行测试，训练模型时设置学习率为0.0004，小批量数据为1，epoch为200。

## 实验结果
###  RICE1

**定性分析**

结果如下，从左到右的图片分别是：多云图像、条件GAN的输出、循环GAN的输出、SpA GAN的输出、真实图像。
![rice1_result](https://github.com/ZYJ-Group/Tanghy/assets/94824386/f0eacf3e-7b45-4e9c-b267-268c53fb2679)  


**定量分析**

|               |  峰值信噪比（PSNR）  | 结构相似性指数（SSIM）  |
| :-----------: | :------------------: | :---------------------: |
|   **条件GAN**    |        26.547        |          0.903          |
| **循环GAN** |        25.880        |          0.893          |
|  **SpA GAN**  |        30.232        |          0.954          |

###  RICE2

**定性分析**

结果如下，从左到右的图片分别是：多云图像、条件GAN的输出、循环GAN的输出、SpA GAN的输出、真实图像。  
![rice2_result](https://github.com/ZYJ-Group/Tanghy/assets/94824386/1e0d2c78-47f7-4afe-ac9e-b71f0f739369)  


**定量分析**

|               |  峰值信噪比（PSNR）  | 结构相似性指数（SSIM）  |
| :-----------: | :------------------: | :---------------------: |
|   **条件GAN**    |        25.384        |          0.811          |
| **循环GAN** |        23.910        |          0.793          |
|  **SpA GAN**  |        28.368        |          0.906          |

