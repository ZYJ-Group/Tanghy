# 合成孔径雷达（SAR） 第一篇（大方向/篇数）
# SAR 图像变化检测传统方法综述 （标题/关键词）
- 谢润博（作者）
- 电脑与信息技术（刊物）
- 链接：[paper](https://github.com/ZYJ-Group/Tanghy/blob/main/1-Literature/SAR%E5%9B%BE%E5%83%8F%E5%8F%98%E5%8C%96%E6%A3%80%E6%B5%8B%E4%BC%A0%E7%BB%9F%E6%96%B9%E6%B3%95%E7%BB%BC%E8%BF%B0.pdf)
- 阅读时间：2023-08-30

### 标题、摘要、关键词、结论
- 标题：SAR 图像变化检测传统方法综述
- 摘要：合成孔径雷达（SAR）卫星具有全天候，全时间对地面情况监测的特点，在获得同一地点多时图像方面有 着巨大优势。变化检测（change detection）是遥感领域中一个重要的应用手段，在洪水监测，建筑物变化监测，农作 物生长情况，地震灾害灾情损失估计等方面有着广泛的应用。如今，合成孔径雷达中的变化检测方法逐渐变成未来 遥感图像研究中的热点。在本文中，对几种合成孔径雷达的传统方法进行比较和分析
- 关键词：合成孔径雷达；变化检测；综述
- 结论：本文首先介绍了变化检测的流程，并说明了 SAR 图像变化检测的意义，之后总结了 SAR 图像变化检 测技术方面的一些常见方法，对近年来的研究中提出 的方法做了介绍。由于 SAR 的获得信息的时效性和 全天候持续获取影像，所以可见其具有很大的潜力的 应用场景。搭载模型的 Android APP，让技术落地，真正帮助到 广大农民朋友，为我国的农业现代化助力。

### 研究背景
- 大背景：在科技不断发展，技术不断进步的背景下，合成 孔径雷达已成为遥感图像研究中的一个热门话题。虽 然光学卫星遥感在危害监测和管理的各个阶段都发挥 着重要作用。
- 小背景：但是由于缺乏足够的采集频率和及时性 的数据，传统的洪水，地震等自然灾害监测遥感仍然 很困难，而合成孔径雷达系统提供了在白天和夜间持 续运行的可能性。

### 研究内容、成果
- 内容：在本文中，重点比较了几种合成孔径雷达变化检 测的传统方法，介绍其变化检测的基本过程原理和实 现过程。
**变化检测流程**
  
SAR 图 像的变化检测分为预处理，变化信息提取以及评价三 个部分。流程图如图 1 所示：

![2023-08-30-01](https://github.com/Axianlatiao/Test/assets/94824386/6c643a42-529a-454b-b236-25b10d02d1c5)

**差异图生成的方法**

  早期的差异图生成算法主要采用最简单的差值 差异运算 , 即直接将两幅 SAR 影像相减。但是 SAR图像的噪声与光学图像不同，主要是由乘性噪声构成， 在文献中提出了差值算法不适用于 SAR 图像。

  在后续的研究中，文献提到，使用对数比算子 (logratio, LR) 生成差异图，这样可以将 SAR 图像内的乘 性噪声转换为加性噪声，并且可以增强变化类和非变 化类的对比度，进一步减少了为变化类背景中一些小 噪声的影响，这个方法可以有效的抑制噪声。

  在文献中提出了均值比算子 (mean-ratio,MR)，该算子利用了 像素的邻域信息，对于单独出现的噪声点有很好的抑 制效果，因为对比的不再是单独的像素点，而是像素 点所在一块区域的均值，但是此算法也有缺点，如果 噪声不是点状而是成片的出现 , 那么 MR 算子可能不 会有很好的效果，这就是其局限性。

  结合上述两种算子的优缺点，在文献中提出了一种使用弧切减法 算子来进行第一步处理生成差分图，之后分别对生成 的差分图进行二维高斯滤波器和中值滤波器进行降噪处理，其中二维高斯滤波器可以保持局部区域像素的 一致性，中值滤波可以处理边缘信息，可以快速的生成最终的差分图

**差异图分析**

  在差异图生成之后，下一步就是对其进行分析， 最终生成一副黑白的二值图。分析常见的方法有两种， 分别是阈值分析和聚类分析。

  （1）阈值法：阈值法是进行阈值筛选来判断出 适用于不同场景的方法，然后将差异图以阈值像素值 为界划分为两类。现在无监督的阈值方法普遍更加使 用，无监督的最优阈值的选择方法中比较经典的有 Kittler&Illingworth(KI) 法 [7] 和 期 望 最 大 化 (expectation maximization，EM) 算法 [8]，这两种方法都需要建立一 个模型来对数据进行拟合，然后通过贝叶斯最小错误 率准则，对两类的概率分析来选出最优的阈值方法。 其中 EM 算法是更具所获取到的数据进行逆推得到模型，且广泛被使用

  （2）聚类法：聚类算法是对生成的差异图进行 聚类操作进行分析，普遍是将图像中的像素分为变化 类，不变类和不确定类，在不确定类中再继续往下进 行分类，通过不同的聚类算法对变化和不变的类进行 变化检测。聚类方法分为硬聚类和模糊聚类两种。 硬聚类以 K 均值 (K-means,KM) 聚类法为代表，模 糊聚类以 (Fuzzy C-means,FCM) 聚类法为代表，硬聚 类 KM 聚类法用贪婪算法推导出，利用类间距离最大和 类内距离最小这两点，通过迭代找到合适的聚类中心但是硬聚类中容易产生一些误差。模糊聚类 FCM 聚 类法在此基础上又加入了模糊集合的概念，可以通过 隶属度这一方法保留更多的原数据特征，使得分类的 准确性有所提高，这也是目前运用很广的聚类方法之 一。在文献中提出了一种以模糊的方式结合局部 空间信息和灰度信息的方法，这种方法被称为模糊 局部信息 c- 均值算法 (FLICM)。FLICM 解决了已知 FCM 算法的缺点，大大提高了聚类的性能

**近年来方法研究**

  自适应离散小波变换与FCM聚类相结合的办法。

- 结果：整体流程通常采用预处理、构造差异图和阈 值分割 3 个步骤进行无监督的影像变化检测

### 总结
- Conclusion by Thy:
  通过一些综述类文章，对SAR先进行初步的了解和认识。

