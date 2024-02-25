## 数据增强 + 迁移学习

### 迁移学习

#### 领域适应（Domain Adaptation）
ADDA
https://github.com/corenel/pytorch-adda

=== Evaluating classifier for encoded target domain ===
>>> source only <<<
Avg Loss = 2924.6131158644152, Avg Accuracy = 68.064517%
>>> domain adaption <<<
Avg Loss = 93.3094972179782, Avg Accuracy = 12.741935%

	MNIST (Source)	USPS (Target)
Source Encoder + Source Classifier	99.140000%	83.978495%
Target Encoder + Source Classifier		97.634409%


#### 小样本学习（Few-shot Learning）
https://github.com/learnables/learn2learn

要掌握这个GitHub上的开源代码“Easy Few-Shot Learning”，你可以按照以下步骤进行：

1. 学习基础知识
如果你是小样本学习的新手，首先应该通过提供的教程笔记本来学习基础知识。这些笔记本包含了从最基础的小样本图像分类入门到更高级的应用和技术。
开始阅读“First steps into few-shot image classification”教程，这是一个小样本学习的基础教程，可以在不到15分钟内快速了解小样本学习的基本概念。
2. 实践和实验
利用提供的“Example of episodic training”和“Example of classical training”笔记本作为起点，设计你自己的小样本学习实验。这些示例将帮助你理解如何使用EasyFSL库进行情景训练和经典训练。
如果你想要直接在嵌入向量上进行推断，可以参考“Test with pre-extracted embeddings”笔记本。这展示了如何一次性提取数据集的所有嵌入向量，然后直接在这些嵌入向量上进行推断，这是许多小样本方法在测试时的常见做法。
3. 了解并使用内置方法
EasyFSL库内置了11种小样本学习方法，包括原型网络（Prototypical Networks）、SimpleShot、匹配网络（Matching Networks）等。尝试理解每种方法的原理，并在你的项目中实验它们。
使用FewShotClassifier类快速开始任何小样本分类算法的实现，并探索常用的架构。
4. 数据加载工具
学习如何使用EasyFSL提供的数据加载工具，例如TaskSampler、FewShotDataset类等，这些工具可以帮助你以小样本分类任务的形式采样实例批次。
5. 探索数据集
熟悉EasyFSL支持的数据集，如CU-Birds、tieredImageNet、miniImageNet和Danish Fungi等。根据提供的指令下载和准备这些数据集，并在你的代码中实例化相应的数据集对象。
6. 安装和设置
安装EasyFSL库，可以通过pip install easyfsl命令或直接克隆仓库。
根据你的需求下载数据，并根据提供的示例笔记本设计你的训练和评估脚本。
7. 参与贡献
如果你在使用过程中遇到问题，可以提出问题(issue)；如果你有新的功能想法或者找到了代码中的错误，也可以贡献你的代码。
8. 复现基准测试
如果你对性能基准测试感兴趣，可以尝试复现库中的基准测试。这需要下载特定的预训练权重，提取测试集的所有嵌入向量，并运行评估脚本。
通过以上步骤，你可以逐步深入了解并掌握Easy Few-Shot Learning库，从而在你的项目中有效地应用小样本学习技术。
