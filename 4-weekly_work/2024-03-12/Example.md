Semantic Segmentation for Remote Sensing based on RGB Images and Lidar Data using Model-Agnostic Meta-Learning and Partical Swarm Optimization
使用模型无关元学习和局部群优化基于 RGB 图像和激光雷达数据的遥感语义分割
2020
IFAC-PapersOnLine
在本文中，我们的主要贡献是MAML在U-Net网络中的创新应用以及使用RGB遥感图像进行训练。 1. MAML用于优化神经网络训练过程。 2.本文采用仿生优化算法来优化神经网络参数更新过程。 3.我们引入激光雷达数据来提高语义分割的准确性。

A Novel Deep Nearest Neighbor Neural Network for Few-Shot Remote Sensing Image Scene Classification
一种用于少镜头遥感图像场景分类的新型深度最近邻神经网络
2023-01-22
Remote Sensing
本文提出了一种基于注意力机制的深度最近邻神经网络（DN4AM）来实现少镜头遥感图像场景分类的端到端框架。我们的方法有三个主要创新。首先，我们的方法引入了一种情景训练方法来训练网络并在新类别上进行测试以进行少样本学习。其次，我们的方法通过具有全局信息的通道注意机制设计与场景类别相关的注意图，以抑制不相关区域的影响。最后，通过场景类相关注意力图对查询图像和类图像之间的局部描述符的相似度进行加权，最终获得图像到类的度量得分，这对于减少场景语义无关的干扰是有意义的对象，以提高分类精度。

A Novel Discriminative Enhancement Method for Few-Shot Remote Sensing Image Scene Classification （以前面那篇做基础改的）
一种新的少镜头遥感图像场景分类判别增强方法
2023-09-18
Remote Sensing 
在本文中，我们提出了基于 DN4AM 模型的判别增强型基于注意力的深度最近邻神经网络（DEADN4）。 DEADN4模型在保留DN4AM优点的同时，还具有三个附加优点。首先，DEADN4模型结合局部和全局信息，采用深度局部全局描述符（DLGD）进行分类，增强了不同类描述符之间的区分。其次，为了增强类内紧凑性，DEADN4引入中心损失来优化全局信息。通过使用中心损失，它将同一类的特征拉向中心，从而有效地增加类内紧凑性，从而减轻显着的类内多样性。最后，DEADN4 通过合并余弦间隔改进了分类模块中的 Softmax 损失函数，鼓励学习特征之间更大的类间距离。这些优点有助于提高小样本 RSISC 结果。

Class-Shared SparsePCA for Few-Shot Remote Sensing Scene Classification 
用于少样本遥感场景分类的类共享 SparsePCA 
2022-05-10 
Remote Sensing 
本文的主要贡献如下。 • 我们使用自监督学习辅助特征提取器训练，因为少镜头遥感场景数据不太可能过度拟合模型问题。通过构建自监督的辅助数据和标签，有效提高了模型性能。 • 我们将子空间学习方法引入到少样本遥感场景分类任务的框架中，并提出了一种新方法：少样本遥感场景分类方法。进一步的实验表明，该方法可以有效解决“负迁移”问题。 • 我们提出了一种基于ClassShared SparsePCA 方法的新颖的少镜头遥感场景分类，称为CSSPCA。 CSSPCA 映射新颖的数据特征映射到更具判别力的子空间以获得更具判别力的重建特征，从而提高分类性能。 • 我们在两个少镜头遥感场景数据集上进行了测试，证明了我们提出的方法的有效性和合理性。

DLA-MatchNet for Few-Shot Remote Sensing Image Scene Classification 
用于少镜头遥感图像场景分类的 
DLA-MatchNet 
9/2021 
IEEE Trans. Geosci. Remote Sensing 
总之，我们提出的模型的主要贡献可以总结如下。 1）通过研究通道间和空间关系，提出了一种具有注意机制的新颖特征学习模块，用于学习少镜头遥感场景图像的鲁棒性和判别性特征表示。 2）我们进一步利用自适应匹配器来测量样本之间的相似性分数，而不是手工制作的固定指标（例如欧几里得距离）。通过匹配器的可学习过程，它可以自适应地处理类内差异和类间相似性问题。 3）三个最先进的遥感图像数据集的实验结果表明我们的模型在场景分类任务中具有引人注目的性能。

Few Shot Scene Classification in Remote Sensing using Meta-Agnostic Machine 
使用元不可知机器对遥感中的少量镜头场景进行分类 
2020 6th Conference on Data Science and Machine Learning Applications (CDMA) 
3/2020 
在本文中，我们针对遥感图像的少镜头分类问题提出了一种改进的元学习解决方案。尽管 MAML 被认为是对小样本学习最有影响力的模型之一，但它存在最大化深度网络灵敏度的问题，这可能导致训练期间的变异性 [13]。我们的方法基于模型不可知元学习（MAML），并修改训练超参数，以实现稳定的训练进度并实现遥感场景分类的高性能和泛化。

Few-Shot Classification of Aerial Scene Images via Meta-Learning 
通过元学习对航空场景图像进行少镜头分类 
2020-12-31 
Remote Sensing 
本文的主要贡献总结如下。 1. 这是第一个提供统一测试平台的工作，以便与航空场景领域的几种最先进的少镜头学习方法进行公平比较。我们的实验评估表明，可以从少量标记图像中学习新类别的大量信息，这对于遥感界来说具有巨大的潜力。 2.所提出的方法包括特征提取模块和元学习模块。首先，ResNet-12 用作主干来学习基本集上输入的表示 fθ。然后，在元训练阶段，我们通过余弦距离和特征空间中可学习的尺度参数来优化分类器，既不固定θ，也不引入任何额外的参数。我们的方法简单而有效，在两个具有挑战性的数据集上实现了最先进的性能：NWPU-RESISC45 和 RSD46-WHU。 3. 我们进行了大量的实验，并从 RSD46-WHU 构建了一个迷你数据集，以进一步研究影响性能的因素，包括数据集规模的影响、不同指标的影响和支持镜头的数量。实验结果表明，我们的模型在少样本设置中特别有效。

Few-Shot Learning for Remote Sensing Image Retrieval With MAML
使用 MAML 进行遥感图像检索的少样本学习
10/2020
2020 IEEE International Conference on Image Processing (ICIP)
本文的主要贡献概括为： 1.基于少样本学习的图像检索的现有工作很少，特别是这个问题的定义需要更加清晰，因此我们在形式上重新定义它。 2.提出了一种基于MAML的少样本学习遥感图像检索方法。结合ResNet和GeM来提取图像特征，并使用基于binning的mAP优化来解决不可微分的mAP问题。 3.在两个遥感影像数据集上验证了该方法的检索有效性和效率

Few-Shot Semantic Segmentation for Building Detection and Road Extraction Based on Remote Sensing Imagery Using Model-Agnostic Meta-Learning
使用与模型无关的元学习，基于遥感图像的建筑物检测和道路提取的少镜头语义分割
2022
Advances in Guidance, Navigation and Control
在本文中，我们的主要贡献是MAML在SegNet和U-Net网络中的创新应用以及使用RGB遥感图像进行训练。对于建筑检测，SegNet应用MAML前后的测试准确率分别为51.73%和56.06%，U-Net应用MAML前后的测试准确率分别为52.54%和57.04%。测试精度分别提高了4.33%和4.5%，对于道路提取，测试精度分别提高了4.47%和7.24%

Learning to Cooperate: Decision Fusion Method for Few-Shot Remote-Sensing Scene Classification
学习合作：少镜头遥感场景分类的决策融合方法
IEEE Geoscience and Remote Sensing Letters
2022
这个简报的主要贡献如下。 1）针对少镜头遥感图像分类任务，提出了一种利用预训练模型作为特征提取器的新方法，有效解决了遥感数据缺乏和模型训练欠拟合的问题。 2）由于预训练数据和遥感数据之间的区别而引起的负迁移问题，我们建议同时使用多个预训练模型，然后融合决策，从而缓解负迁移问题。同时，我们提出了决策注意模块，为各种决策赋予不同的权重。 3) 制造设计 (DFM) 是一种简单而有效的方法，它融合了从不同预训练模型中获得的决策。更强大的特征表示和决策融合使 DFM 能够表现出惊人的性能。我们认为DFM在现实中应用可能是有意义的。

Meta-FSEO: A Meta-Learning Fast Adaptation with Self-Supervised Embedding Optimization for Few-Shot Remote Sensing Scene Classification
Meta-FSEO：一种具有自监督嵌入优化的元学习快速适应，用于少镜头遥感场景分类
Remote Sensing
2021-07-14
本文在三个主要方面对文献做出了贡献：(1)我们提出了一种称为Meta-FSEO的元学习算法，以提高少样本场景下多种城市条件下分类模型的泛化性能。所提出的 Meta-FSEO 通过根据任务级样本对已知城市的数据进行训练，可以快速概括来自未知城市的数据。 （2）我们设计了一个自监督比较模块，可以有效平衡不同时间和地点收集的多个图像之间的特征分类任务的要求。 （3）我们设计了一种结合了对比度损失和交叉熵损失加权的损失函数，旨在实现高精度的泛化能力。

Meta-Learning for Few-Shot Land Cover Classification
用于少样本土地覆盖分类的元学习
2020 IEEE/CVF Conference on Computer Vision and Pattern Recognition Workshops (CVPRW)
6/2020
我们的主要贡献是（1）证明跨地域的遥感任务可以重构为一个元学习问题，以及（2）评估 MAML 对多光谱和高分辨率遥感图像的少样本分类和分割；具体来说，是被广泛引用的基准数据集 Sen12MS 和 DeepGlobe。

MMML: Multimanifold Metric Learning for Few-Shot Remote-Sensing Image Scene Classification
MMML：用于少镜头遥感图像场景分类的多流形度量学习
IEEE Transactions on Geoscience and Remote Sensing
2023
我们的贡献可总结如下。 1）我们提出了一个结合了 CNN 和 MMML 的小样本 RSSC 框架。在该框架中，融合了基于CNN局部特征的两个异构且互补的黎曼流形特征，以增强表示能力。在不同的流形空间上定义两个原型作为类别的表示，并探索整合它们的最佳权重因子。 2）我们设计了一种可学习的距离度量方案，可以根据类间对和类内对的分歧进行优化。类间散度与类内散度之比作为计算距离的优化函数，我们应该最大化它，从而减少较大的类内差异和较高的类间相似度对场景识别的影响。 3）我们对三个公共数据集进行了比较实验，以研究我们提出的方法的性能。结果表明，MMML 在小样本 RSSC 任务中优于以前的方法。

Multi-attention DeepEMD for Few-Shot Learning in Remote Sensing
用于遥感中少样本学习的多注意 DeepEMD
2020-12-11
2020 IEEE 9th Joint International Information Technology and Artificial Intelligence Conference (ITAIC)
本文的主要贡献如下。 1.提出了一种注意力参考机制来计算推土机距离所需的权重。 2.通道和空间注意力模块用于增强模型提取特征的能力。 3.引入标签平滑以避免过拟合。

Research Progress on Few-Shot Learning for Remote Sensing Image Interpretation ★
遥感图像解译的少样本学习研究进展
2021
IEEE J. Sel. Top. Appl. Earth Observations Remote Sensing
鉴于对遥感图像解译的少样本学习缺乏全面的综述，我们通过对现有作品的详细文献计量分析，对相关研究进行了全面的回顾，从数据的角度系统地回顾了少样本学习方法增强和知识重用，并讨论遥感图像解释的少样本学习的几个有前途的未来方向。本文可为从事遥感领域少样本学习研究的学者提供参考。
与基于迁移学习的方法相比，基于元学习的方法可以训练适用于多个任务的元模型，具有快速适应的特点。该方法避免了在迁移学习中手动选择相关性高的源域数据。此外，元学习可以与多种模型集成，用于分类、回归和强化学习。由于这些优点，元学习成为遥感图像解释的小样本学习的理想范例。然而，该方法的一个局限性是元学习需要具有丰富类别多样性的辅助数据集以保证元模型的泛化能力。然而，现有的公开遥感数据集仅包含少量地理空间对象类别。数据集的高要求严重限制了元学习算法的应用。

RS-MetaNet: Deep meta metric learning for few-shot remote sensing scene classification
RS-MetaNet：用于少镜头遥感场景分类的深度元度量学习
8/2021
IEEE Trans. Geosci. Remote Sensing
总之，这项工作提供了三个贡献： • 我们提出了一种称为 RS-MetaNet 的新颖框架，以提高少样本遥感场景分类的性能。 RS-MetaNet 通过元任务训练模型，这迫使我们的模型学习任务级分布，该分布应该更好地推广到未见过的测试任务。 • 我们提出了一种新的损失函数，称为平衡损失，它将最大泛化损失与交叉熵损失函数结合起来。在损失的约束下，RS-MetaNet通过最大化不同类别之间的距离，最大化模型对新样本的泛化能力，为不同类别的场景提供更好的线性分割平面，同时保证模型拟合。 • 我们的度量模块使用可学习的距离度量，允许RS-MetaNet 充分利用数据本身的信息，使学习的度量空间更具辨别力。

SCL-MLNet: Boosting Few-Shot Remote Sensing Scene Classification via Self-Supervised Contrastive Learning
SCL-MLNet：通过自监督促进少样本遥感场景分类
2022
IEEE Trans. Geosci. Remote Sensing
总而言之，我们的主要贡献如下。 1）我们提出了一种名为SCL-MLNet的端到端多任务框架，用于通过SCL模块进行少镜头遥感场景分类。与现有的few-shot方法不同，SCL-MLNet可以使用数据中的信息和标签作为监督信号。2）基于SCL-MLNet，我们设计了一种新颖的损失函数，可以通过赋予适当的权重系数来平衡SCL损失和少样本分类损失。 3）考虑到类内分类目标大小不同的情况，我们引入了一种新颖的注意力模块来融合不同大小的分类目标的多尺度特征，以丰富视觉表示，具有即插即用和可扩展的特点。 4）与代表性的少样本学习方法相比，我们在三个广泛使用的遥感场景分类数据集上实现了最先进的性能。


Semi-Supervised Hyperspectral Image Classification via Spatial-Regulated Self-Training
通过空间调节自训练进行半监督高光谱图像分类
Remote Sensing
2020-01-02
总之，本文的贡献可概括如下： • 我们引入了一种基于深度学习模型与聚类遥感协作的新型 HSIc 半监督分类算法。  • 相邻高光谱图像中的像素可能属于同一类。我们在上述算法中引入了空间约束来给出平滑度假设以提高 HSIc 的准确性。 • 与以前的方法相比，我们提出的方法在利用微小标记数据的同时，在HSIC 上实现了具有竞争力的性能。

Self-Taught Feature Learning for Hyperspectral Image Classification
高光谱图像分类的自学特征学习
5/2017
IEEE Trans. Geosci. Remote Sensing
在本文中，我们提出了两种不同的 HSI 分类自学学习框架：1）多尺度 ICA（MICA）和 2）堆叠卷积自动编码器（SCAE）。两个模型都从不同的集合中学习一组可泛化的过滤器未标记的 HSI 数据，但 MICA 学习低级特征表示，而 SCAE 学习更深层次的特征。然后应用这些过滤器对三个流行的标记 HSI 基准数据集进行分类：Indian Pines、Salinas Valley 和 Pavia University。尽管这些数据集具有不同的 GSD，但我们表明 MICA 和 SCAE 仍然能够产生最先进的结果。我们还证明它们的特征可以通过频带重采样跨不同的传感器转移。

MugNet: Deep learning for hyperspectral image classification using limited samples
MugNet：使用有限样本进行高光谱图像分类的深度学习
ISPRS Journal of Photogrammetry and Remote Sensing
11/2018
MugNet的主要贡献可以概括如下：针对小规模数据分类，开发了基于深度学习的HSI分类方法。与一些最先进方法的对比实验验证了 MugNet 的有效性。为了提高分类性能，MugNet 提出了三种新颖的策略，即多粒度扫描、半监督学习和简单的基本框架。

Low-Shot Learning for the Semantic Segmentation of Remote Sensing Imagery
遥感图像语义分割的低镜头学习
IEEE Transactions on Geoscience and Remote Sensing
2018
本文的主要贡献如下。 1）我们描述了用于非RGB遥感图像中空间光谱特征提取的堆叠多损失卷积自动编码器（SMCAE）模型（见图4）。 SMCAE 使用无监督自学学习来获取大量特征提取器。 SuSA 使用 SMCAE 进行特征提取。 2）我们提出了半监督多层感知器（SS-MLP）模型（见图5）用于非RGB遥感图像的语义分割。 SuSA 使用 SS-MLP 对 SMCAE 的特征表示进行分类，SS-MLP 的半监督机制使其能够在低样本学习中表现良好。 3) 我们证明 SuSA 在 IEEE GRSS 数据和算法标准评估 (DASE) 网站上托管的 Indian Pines 和 Pavia 大学数据集上取得了最先进的结果。

