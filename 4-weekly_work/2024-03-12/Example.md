2024

IEEE Journal of Selected Topics in Applied Earth Observations and Remote Sensing  
Research Progress on Few-Shot Learning for Remote Sensing Image Interpretation  
遥感图像解译的少样本学习研究进展  


DLA-MatchNet for Few-Shot Remote Sensing Image Scene Classification  
IEEE Transactions on Geoscience and Remote Sensing  
用于少镜头遥感图像场景分类的 DLA-MatchNet  
总之，我们提出的模型的主要贡献可以总结如下。 1）通过研究通道间和空间关系，提出了一种具有注意机制的新颖特征学习模块，用于学习少镜头遥感场景图像的鲁棒性和判别性特征表示。 2）我们进一步利用自适应匹配器来测量样本之间的相似性分数，而不是手工制作的固定指标（例如欧几里得距离）。通过匹配器的可学习过程，它可以自适应地处理类内差异和类间相似性问题。 3）三个最先进的遥感图像数据集的实验结果表明我们的模型在场景分类任务中具有引人注目的性能。  

![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/08987c40-06af-496e-9be4-bfc8ac28bebb)  


IEEE Transactions on Geoscience and Remote Sensing  
Dual Contrastive Network for Few-Shot Remote Sensing Image Scene Classification  
用于少镜头遥感图像场景分类的双对比网络  
概括起来，主要亮点有四个。 1）我们提出了FS-RSISC的DCN，它由CCL和DCL组成。它使模型能够通过两个对比学习分支之间的互补性来提取判别性和细节特征。 2）我们为CCL设计了一个冷凝器网络，它通过利用全局上下文生成有区别的上下文特征来增强与场景相关的信息。 3）为DCL设计了冶炼厂网络，它通过自适应定位重要的局部图像区域来提取细节特征。 4）我们的 DCN 在四个基准遥感数据集上实现了具有竞争力的性能，甚至在 NWPU-RESISC45 [27] 和 AID [28] 数据集上的五个数据集上比最先进的方法至少高出 3.56% 和 5.38%分别为五路射击。  


IEEE Geoscience and Remote Sensing Letters  
Few-Shot Object Detection of Remote Sensing Images via Two-Stage Fine-Tuning  
通过两阶段微调进行遥感图像少镜头目标检测  
这封简报中提供的主要贡献如下，1）我们提出了一种具有基于对合主干的两阶段少样本检测器，该检测器在基类上进行了全面训练，以在第一阶段提取信息，并在小型平衡数据集上进行部分微调以推广到新类别在第二阶段。 2）PAM旨在建立用于预测多尺度对象的特征金字塔。 3）通过形状偏差实现检测性能的提高，无需额外成本。  

IEEE Transactions on Geoscience and Remote Sensing  
Few-Shot Object Detection on Remote Sensing Images  
遥感图像上的少样本目标检测  
本文的主要贡献总结如下。 1）在本文中，我们介绍了第一个基于元学习的遥感小样本目标检测方法。我们的方法使用一些已见类别的大规模数据进行训练，并且可以学习有关对象检测的元知识，因此只需少量标记样本即可很好地推广到未见类别。 2）我们的方法包含三个主要组件：元特征提取网络、特征重新加权模块和边界框预测模块。所有三个模块均采用多尺度架构设计，以实现多尺度目标检测。 3）在两个公共基准数据集上的实验证明了所提出的方法在遥感图像上少镜头目标检测方面的有效性。  

IEEE Journal of Selected Topics in Applied Earth Observations and Remote Sensing  
Few-Shot Object Detection With Self-Adaptive Attention Network for Remote Sensing Images  
遥感图像中自适应注意力网络的少样本目标检测  
本文的主要贡献如下。 1）我们提出了一种基于两级检测器的少镜头对象检测器，该检测器专注于对象级关系，以适应对象检测任务中可用的对象级数据。 2）我们实现了一个关系门循环单元（GRU）单元来获取对象级关系，并同时在支持图像的帮助下对对象特征添加额外的关注。 3）我们选择迁移学习来代替元学习，以减轻训练过程的难度，以充分利用基类数据中的信息。  

IEEE Transactions on Geoscience and Remote Sensing  
Few-Shot Scene Classification of Optical Remote Sensing Images Leveraging Calibrated Pretext Tasks  
利用校准借口任务的光学遥感图像少镜头场景分类  
总之，我们工作的主要贡献可以总结如下。 1）据我们所知，我们的工作是利用多个借口任务的几次遥控场景分类的首次尝试。我们通过设计辅助目标及其协同作用，在遥感主题中为几乎没有的学习提供了新的灯光。 2）我们在几次学习任务中证明了AMP正则化技术的利用是合理的，这有助于网络培训并改善所得的性能。 3）我们进行了广泛的实验，以证明我们的多任务学习框架的有效性并验证每种成分的贡献。我们表明，我们的框架在公共遥感数据集上取得了最佳性能，包括西北理工大学（NWPU）-Resisc45 [5]，空中图像数据集（AID），[55]和Wuhan University（Wuhan University（WHU） -  remote Sensing（RS-remote Sensing（RS） ）-19 [6]。  

ISPRS Journal of Photogrammetry and Remote Sensing  
Generalized few-shot object detection in remote sensing images（有[代码](https://github.com/RSer-XDU/G-FSDet)）  
遥感图像中的广义少样本目标检测  
本文的主要贡献可以概括如下： 1.通过对预训练检测器中不同组件的综合分析，提出了一种高效的迁移学习框架，更适合少样本地理空间目标检测。 2. 基于度量的判别损失旨在在微调阶段增强类内紧凑性和类间可分离性，从而在少镜头场景中产生更具判别力的分类器。 3. 据我们所知，本文是遥感界第一篇专注于G-FSOD任务的工作，并设计了表示补偿模块来解决基类的灾难性遗忘问题。 4. 我们提出的 G-FSDet 实现了两个遥感 FSOD 基准的最先进的整体性能，它在少样本新颖类中获得了有竞争力的性能，而基类性能略有下降。  
  

International Journal of Applied Earth Observation and Geoinformation  
HCPNet: Learning discriminative prototypes for few-shot remote sensing image scene classification  
HCPNet：学习用于少镜头遥感图像场景分类的判别原型  
总而言之，我们对该领域的主要贡献如下： • 我们的方法涉及开发混合对比原型网络（HCPNet）来学习处理 FSRSSC 中类别混淆问题的紧凑且有区别的原型。 • 我们为 FS-RSSC 提出了一种新颖的元学习范例，它将查询特征合并到原型表示中，并用两种新颖的对比损失对其进行正则化：QPC 损失和 PPC 损失。这些损失是针对 FS-RSSC 任务量身定制的，并通过新颖的基于情节的对比学习框架进行了优化。 • 当在四个 FS-RSSC 数据集上进行评估时，我们的网络在一般的少样本分类和域泛化设置方面都超越了现有方法。 • 我们设计的网络能够以无缝的端到端方式轻松训练，无需额外信息或增加模型复杂性。  

IEEE Geoscience and Remote Sensing Letters  
Learning to Cooperate: Decision Fusion Method for Few-Shot Remote-Sensing Scene Classification  
学习合作：少镜头遥感场景分类的决策融合方法  
这个简报的主要贡献如下。 1）针对少镜头遥感图像分类任务，提出了一种利用预训练模型作为特征提取器的新方法，有效解决了遥感数据缺乏和模型训练欠拟合的问题。 2）由于预训练数据和遥感数据之间的区别而引起的负迁移问题，我们建议同时使用多个预训练模型，然后融合决策，从而缓解负迁移问题。同时，我们提出了决策注意模块，为各种决策赋予不同的权重。 3) 制造设计 (DFM) 是一种简单而有效的方法，它融合了从不同预训练模型中获得的决策。更强大的特征表示和决策融合使 DFM 能够表现出惊人的性能。我们认为DFM在实际应用中可能有意义。  

IEEE Transactions on Geoscience and Remote Sensing  
Progressive Parsing and Commonality Distillation for Few-Shot Remote Sensing Segmentation  
少镜头遥感分割的渐进解析和共性蒸馏  
我们的主要贡献如下。 1）为了解决低数据条件下的遥感场景分割问题，我们设计了一个概念简单且易于实现的框架，称为PCNet。 2）提出的两个关键组件，即渐进解析模块（PPM）和共性蒸馏模块（CDM），相辅相成，以纠正不完整对象和不相关干扰项的频繁出现。 3）我们在标准数据集上进行了大量的实验来验证所提出的框架，该框架在多种设置下实现了最先进的性能。  


IEEE Trans. Geosci. Remote Sensing  
Prototype-CNN for Few-Shot Object Detection in Remote Sensing Images  
用于遥感图像中少样本目标检测的Prototype-CNN  
总而言之，我们的贡献有四重。首先，我们提出了一种新颖的 P-CNN 框架，专为遥感图像中的少样本目标检测而设计。其次，我们提出的方法利用 PLN 提供类感知原型进行指导，并利用原型引导的 RPN 来突出显示前景对象的区域，这可以为检测头提供更好的建议。第三，我们通过相当简单的多方向样本增强操作考虑了方向变化的问题，从而增强了模型处理物体任意方向问题的能力。第四，我们首次在大规模 DIOR 数据集上为少样本检测任务构建了四种不同的新颖/基础分割设置，并展示了基线结果以供进一步研究。  
  

IEEE Transactions on Geoscience and Remote Sensing  
RS-MetaNet: Deep meta metric learning for few-shot remote sensing scene classification  
RS-MetaNet：用于少镜头遥感场景分类的深度元度量学习  
总之，这项工作提供了三个贡献： • 我们提出了一种称为 RS-MetaNet 的新颖框架，以提高少镜头遥感场景分类的性能。 RS-MetaNet 通过元任务训练模型，这迫使我们的模型学习任务级分布，该分布应该更好地推广到未见过的测试任务。 • 我们提出了一种新的损失函数，称为平衡损失，它将最大泛化损失与交叉熵损失函数结合起来。在损失的约束下，RS-MetaNet通过最大化不同类别之间的距离，最大化模型对新样本的泛化能力，为不同类别的场景提供更好的线性分割平面，同时保证模型拟合。 • 我们的度量模块使用可学习的距离度量，允许RS-MetaNet 充分利用数据本身的信息，使学习的度量空间更具辨别力。  

IEEE Transactions on Geoscience and Remote Sensing  
SCL-MLNet: Boosting Few-Shot Remote Sensing Scene Classification via Self-Supervised Contrastive Learning  
SCL-MLNet：通过自监督对比学习促进少样本遥感场景分类  
总而言之，我们的主要贡献如下。 1）我们提出了一种名为SCL-MLNet的端到端多任务框架，用于通过SCL模块进行少镜头遥感场景分类。与现有的few-shot方法不同，SCL-MLNet可以使用数据中的信息和标签作为监督信号。2）基于SCL-MLNet，我们设计了一种新颖的损失函数，可以通过赋予适当的权重系数来平衡SCL损失和少样本分类损失。 3）考虑到类内分类目标大小不同的情况，我们引入了一种新颖的注意力模块来融合不同大小的分类目标的多尺度特征，以丰富视觉表示，具有即插即用和可扩展的特点。 4）与代表性的少样本学习方法相比，我们在三个广泛使用的遥感场景分类数据集上实现了最先进的性能。  


IEEE Journal of Selected Topics in Applied Earth Observations and Remote Sensing  
Semisupervised Few-Shot Remote Sensing Image Classification Based on KNN Distance Entropy  
基于KNN距离熵的半监督少样本遥感图像分类  
因此，本研究的主要贡献可总结如下。 1）本工作聚焦于面向识别任务的遥感图像质量评估，提出采用KNN距离熵作为评估指标来筛选高信息量数据。实验结果表明，少样本条件下的高质量数据是核心集样本而不是边界样本。换句话说，当数据预算有限时，优先选择核心集数据采集和传输。 2）我们提出了一种新颖的半监督学习方法，该方法从未标记集中筛选出具有较小KNN距离熵的高置信度样本，并自动为它们分配高质量的伪标签。有效提高了少样本实验结果。 3）进行了多次元任务实验来比较平均测试精度和元任务误差幅度。还深入讨论了少样本参数设置、数据规模和半监督参数的影响。  


IEEE Transactions on Geoscience and Remote Sensing  
SPNet: Siamese-Prototype Network for Few-Shot Remote Sensing Image Scene Classification  
SPNet：用于少镜头遥感图像场景分类的连体原型网络  
总而言之，我们的贡献如下。 1）基于原型网络，我们提出了一种新颖的原型SC方法，它可以带来更多的监督来学习准确的原型，而无需添加任何可学习的参数。 2）通过IC方法，我们可以获得查询样本更准确的预测概率，从而隐式地进一步校准原型。两个Siamese原型的IC为模型做出更好的分类提供了更具代表性的信息。 3）我们在三个公共遥感数据集上演示了我们的方法，我们的模型在少镜头遥感图像场景分类任务中,结果显示出出色的性能。  
