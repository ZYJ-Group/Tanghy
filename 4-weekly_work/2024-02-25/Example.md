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
