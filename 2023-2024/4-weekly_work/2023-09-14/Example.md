# SAR（大方向/篇数）
### 主要任务  
  SAR图像辅助光学图像去云，但是生成的图像实际上有一些错误信息。利用SAR和光学图像的时序数据，纠正生成图像中的错误信息。

---

### 阶段任务    
1. 检索论文
谷歌学术搜索关键词，分辨论文的好坏，判断遥感领域好的期刊。  
2. 清楚流程
它们的输入输出是什么，用的什么数据集，数据集有哪些特点。

### 初步了解  
**检索论文**  
步骤：
  1. 在谷歌学术上搜索相关关键词，如 "遥感领域"，以找到相关论文。
  2. 阅读摘要和关键词以初步分辨论文的相关性。
  3. 查看每篇论文的引用数量和被引用的频率，这可以表明论文的影响力。
  4. 查看作者的背景和研究机构，以确定论文的可信度。
  5. 检查论文发表的期刊，特别是知名的遥感领域期刊，以评估论文的质量。
  6. 注意论文的出版日期，确保它们是最新的研究成果。

较好的期刊：
期刊名称	| 出版商/机构	| 网站链接
--- | --- | ---
Remote Sensing of Environment	| Elsevier |	[链接](https://www.journals.elsevier.com/remote-sensing-of-environment)
IEEE Transactions on Geoscience and Remote Sensing |	IEEE |	[链接](https://www.ieee.org/publications/rights/Geoscience-and-Remote-Sensing.html)
International Journal of Remote Sensing	| Taylor & Francis |	[链接](https://www.tandfonline.com/toc/tres20/current)
Journal of Applied Remote Sensing	 | SPIE |	[链接](https://www.spiedigitallibrary.org/journals/journal-of-applied-remote-sensing)
ISPRS Journal of Photogrammetry and Remote Sensing	| Elsevier |	[链接](https://www.journals.elsevier.com/isprs-journal-of-photogrammetry-and-remote-sensing)
Journal of Remote Sensing |	China National Committee for Remote Sensing |	[链接](http://www.jors.cn/EN/volumn/home.shtml)
Remote Sensing	| MDPI |	[链接](https://www.mdpi.com/journal/remotesensing)

**清楚流程**  
   
  1. 数据收集：首先，确保你有足够的SAR图像和光学图像数据来进行分析。这些数据可以来自卫星、飞机或其他传感器。

  2. 数据预处理：对SAR图像和光学图像进行预处理，包括去噪、辐射校正和几何校正等。这可以帮助提高图像质量和准确性。

  3. 图像配准：将SAR图像和光学图像进行配准，以确保它们在时间和空间上对齐。这是为了后续的时序分析做准备。

  4. 时序分析：使用时序SAR图像和光学图像数据，例如时间序列分析方法，来检测和纠正图像中的错误信息。这可以涉及到检测云覆盖、大气校正、阴影校正等。

  5. 机器学习和深度学习：利用机器学习和深度学习技术来自动检测和纠正错误信息。可以使用卷积神经网络（CNN）等方法来训练模型，以识别和修复图像中的问题。

  6. 结果评估：对纠正后的图像进行评估，确保它们满足项目要求。可以使用指标如信噪比（SNR）和结构相似性指数（SSIM）来评估图像质量。

  7. 报告和沟通：向项目团队和周老师汇报你的工作，解释你采取的方法和得到的结果。如果需要进一步的改进或调整，根据反馈进行修改。

  8. 持续优化：根据反馈和项目的需求，持续优化和改进图像纠正方法，以确保最佳的结果。

  这个项目涉及到遥感图像处理和时序分析，可能需要一定的计算机视觉和数据科学知识。
