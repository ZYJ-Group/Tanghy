# 遥感影像处理工具和方法

## 1. [segment-anything-eo/segment-geospatial](https://github.com/opengeos/segment-geospatial)

### 1.1 segment-geospatial

#### 1.1.1 目的

`segment-geospatial` 是一个用于使用 Segment Anything Model (SAM) 对地理空间数据进行分割的 Python 包。该包旨在简化使用 SAM 进行地理空间数据分析的过程，使用户能够以最小的编程工作实现这一目标。

#### 1.1.2 方法

`segment-geospatial` 从由 Aliaksandr Hancharenka 编写的 `segment-anything-eo` 仓库中汲取灵感。为了方便 SAM 用于地理空间数据，我开发了 `segment-anything-py` 和 `segment-geospatial` Python 包，这两个包现在可以在 PyPI 和 conda-forge 上获得。我主要的目标是通过使用户能够以最小的编程工作来实现 SAM 的地理空间数据分析，从而简化这个过程。我从 `segment-anything-eo` 仓库的源代码中改编了 `segment-geospatial` 的源代码，原始版本由 Aliaksandr Hancharenka 创作。

- **自由软件：** MIT 许可证
- **文档：** [https://samgeo.gishub.org](https://samgeo.gishub.org)

#### 1.1.3 [示例](https://github.com/opengeos/segment-geospatial#examples)

- 分割遥感图像
- 自动生成对象掩模
- 使用文本提示分割遥感图像
- 使用框提示分割遥感图像
- 使用文本提示批量分割
- 与 ArcGIS Pro 一起使用 `segment-geospatial`
- 使用文本提示分割游泳池
- 从 Maxar Open Data Program 分割卫星图像

## 2. [samrs](https://github.com/ViTAE-Transformer/SAMRS)

### 2.1 Scaling-up Remote Sensing Segmentation Dataset with Segment Anything Model

#### 2.1.1 目的

这是论文《Scaling-up Remote Sensing Segmentation Dataset with Segment Anything Model》的官方存储库。在这项研究中，我们利用SAM和现有的RS目标检测数据集开发了一个高效的流程，生成了一个大规模的RS分割数据集，命名为SAMRS。SAMRS在规模上超过了现有的高分辨率RS分割数据集几个数量级，并提供了可用于语义分割、实例分割和目标检测的对象类别、位置和实例信息，可以单独或组合使用。我们还从各个方面对SAMRS进行了全面的分析，希望能促进RS分割领域的研究，特别是在大型模型预训练方面。

#### 2.1.2 方法

请参见 [Generate Dataset](https://github.com/ViTAE-Transformer/SAMRS/tree/main/Generate%20Dataset) 获取生成SAMRS数据集的代码。

#### 2.1.3 结果

**生成数据集的基本信息**

![Comparisons of different high-resolution RS segmentation datasets.](Figure_Comparisons_Link)

我们在表格中与现有高分辨率RS分割数据集进行了SAMRS数据集的比较。基于现有的高分辨率RS目标检测数据集，我们能够高效地标注10,5090张图像，这是现有数据集容量的十倍以上。此外，SAMRS继承了原始检测数据集的类别，使它们比其他高分辨率RS分割集合更加多样化。值得注意的是，由于在RSI中标记像素的难度，RS目标数据集通常比RS分割数据集具有更多样化的类别，因此我们的SAMRS缩小了这一差距。

**生成掩码的可视化**

![Some visual examples from the three subsets of our SAMRS dataset.](Figure_Visual_Examples_Link)

在图中，我们展示了SAMRS数据集三个子集的一些分割注释的可视化示例。可以看出，SOTA对小型汽车具有更多的实例，而FAST对SOTA中的汽车、船和飞机等现有类别提供了更精细的注释。另一方面，SIOR为更多不同的地面对象（如水坝）提供了注释。因此，我们的SAMRS数据集涵盖了各种大小和分布的类别，为RS语义分割提供了新的挑战。

## 3. [RSPrompter](Link_to_RSPrompter)

### 3.1 Scaling-up Remote Sensing Segmentation Dataset with Segment Anything Model

#### 3.1.1 目的

本文旨在设计一种基于Segment Anything Model（SAM）基础模型的自动化遥感图像实例分割方法，同时整合语义类别信息。提出的方法命名为RSPrompter。通过受到提示学习的启发，引入了一种学习生成适当提示的方法，以使SAM能够为遥感图像生成语义可辨别的实例分割结果。

#### 3.1.2 方法

- **SAM 基础模型扩展：** 在SAM的图像编码器之后添加了一个实例分割头，以适应遥感图像实例分割任务。
- **SAM "everything" 模式：** 通过SAM的“everything”模式生成图像中所有对象的掩码，然后通过分类器对其进行分类为特定类别。
- **目标检测引导 SAM：** 使用目标检测器生成对象边界框，将其作为先验提示输入到SAM中，以获取相应的实例分割掩码。
- **RSPrompter 方法：** 提出了RSPrompter，该方法为即时分割掩码创建与类别相关的提示嵌入。模型参数在此部分被保持冻结。

#### 3.1.3 结果

通过在WHU建筑、NWPU VHR-10和SSDD数据集上进行大量实验证明了RSPrompter方法的有效性。通过可视化分析，RSPrompter相对于其他SAM-based技术和最先进的实例分割方法，在实例分割方面取得了显著的视觉改进。与替代方法相比，RSPrompter生成了更优异的结果，表现出更清晰的边缘、更明显的轮廓、更完整的结果，并更接近地面实况的参考。

