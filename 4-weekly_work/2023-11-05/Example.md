# BIT Reproduction

# 模型评估指标：精度、召回率和F1分数

## 精度（Precision）

精度是指在所有被模型预测为正类别的样本中，实际上是正类别的比例。精度可以用以下公式表示：

$\text{Precision} = \frac{\text{True Positives}}{\text{True Positives + False Positives}}\$

精度衡量了模型在预测为正类别的样本中的准确性。

## 召回率（Recall）

召回率是指在所有实际正类别的样本中，被模型正确预测为正类别的比例。召回率可以用以下公式表示：

$\text{Recall} = \frac{\text{True Positives}}{\text{True Positives + False Negatives}}$

召回率衡量了模型对正类别样本的覆盖程度。

## F1分数（F1 Score）

F1分数是精度和召回率的调和平均数，可以通过以下公式计算：

$F1 = \frac{2 \times \text{Precision} \times \text{Recall}}{\text{Precision + Recall}}$

F1分数综合考虑了模型的准确性和覆盖性。它特别适用于处理不平衡类别的情况，其中正类别和负类别的样本数量差异较大。

这些指标通常用于评估二分类模型的性能，但也可以扩展到多分类问题。在评估模型性能时，了解这些指标有助于全面了解模型在不同方面的表现。

# 实验结果
| 数据集 (Dataset) | running_mf1 | Accuracy (acc) | Mean IoU (miou) | Mean F1 (mf1) | IoU Class 0 | IoU Class 1 | F1 Class 0 | F1 Class 1 | Precision Class 0 | Precision Class 1 | Recall Class 0 | Recall Class 1 |
|-----------------|--------------|-----------------|-----------------|--------------|--------------|--------------|-------------|-------------------|-------------------|-----------------|-----------------| ----------
| LEVER             | 0.57380      | 0.94999         | 0.48876         | 0.51402      | 0.94991      | 0.02760      | 0.97431      | 0.05372     | 0.95037           | 0.74612           | 0.99949         | 0.02786         |
| DSIFN           | 0.49727      | 0.98781         | 0.49465         | 0.49842      | 0.98781      | 0.00149      | 0.99387      | 0.00298     | 0.98791           | 0.15170           | 0.99990         | 0.00151         |
| S2Looking       | 0.72377      | 0.98786         | 0.59416         | 0.66394      | 0.98783      | 0.20049      | 0.99388      | 0.33401     | 0.99088           | 0.49728           | 0.99689         | 0.25145         |

# 评估指标解释

- **running_mf1:** 正在运行的 F1 分数。
- **Accuracy (acc):** 准确率，表示模型正确分类的样本比例。
- **Mean IoU (miou):** 平均交并比（Mean Intersection over Union），用于衡量图像分割任务中模型的性能。
- **Mean F1 (mf1):** 平均 F1 分数。
- **IoU Class 0 和 IoU Class 1:** 分别表示类别 0 和类别 1 的交并比。
- **F1 Class 0 和 F1 Class 1:** 分别表示类别 0 和类别 1 的 F1 分数。
- **Precision Class 0 和 Precision Class 1:** 分别表示类别 0 和类别 1 的精度。
- **Recall Class 0 和 Recall Class 1:** 分别表示类别 0 和类别 1 的召回率。

这些指标用于评估模型在分类和图像分割任务中的性能，提供了关于准确性、覆盖性和精细度的详细信息。Markdown格式可以方便地用于文档和报告。

