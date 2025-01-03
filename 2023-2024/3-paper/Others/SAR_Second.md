# 合成孔径雷达（SAR） 第二篇（大方向/篇数）
# Grassland mowing event detection using combined optical, SAR, and weather time series （标题/关键词）
- Holtgrave，Ann-Kathrin（作者）
- Remote Sensing of Environment（刊物）
- 链接：[paper](https://github.com/ZYJ-Group/Tanghy/blob/main/1-Literature/Grassland%20mowing%20event%20detection%20using%20combined%20optical%2C%20SAR%2C%20and%20weather%20time%20series.pdf)
- 阅读时间：2023-09-15

### 标题、摘要、关键词、结论
- **标题**：使用组合光学、SAR 和天气时间序列进行草原割草事件检测
- **摘要**：欧盟共同农业政策 (CAP) 和栖息地指令旨在改善农业景观的生物多样性。这两项政策都需要大量的监测，而遥感可以促进监测。通过割草频率衡量的使用强度是永久草原生物多样性的重要指标。割草的频率和时间可以使用卫星遥感来确定，因为光合活性生物量响应割草而迅速变化。然而，草的快速再生需要非常密集的卫星时间序列才能进行可靠的检测。雷达时间序列可以补充光学时间序列并填补云相关的空白来克服这个问题。额外的天气数据可以支持草原割草事件的检测，因为割草事件与特定的气象条件相关。然而，之前的研究尚未充分利用这两种潜力或不同的机器学习方法来检测割草事件。本研究提出了一种新的可转移两步方法，利用组合光学和 SAR 数据以及附加天气数据来检测草地割草事件。首先，我们使用光学和 SAR 数据的监督机器学习回归来填补光学时间序列中与云相关的空白。然后，我们使用四种不同的机器学习算法将光学、SAR 和天气数据的时间序列分为已割草和未割草。我们使用了 NDVI 和 EVI（结合 Sentinel-2 和 Landsat 8）的时间序列、SAR 反向散射、六天干涉相干性、反向散射雷达植被指数、反向散射交叉比 (Sentinel-1) 以及温度和降水总和。我们的测试地点分布在德国各地，覆盖整个草原利用强度梯度。割草事件的 F1 值高达 89%，首次割草事件的检测率高达 94%。我们的结果表明，与线性插值时间序列相比，用机器学习填充时间序列没有结构优势。 Sentinel-2 和 Landsat-8 时间序列的组合提供了密集的时间序列，其中值间隔大多小于 20 天，这证明足以可靠地检测割草事件。在我们的研究中，SAR 数据对于割草事件检测并不重要，但天气数据改进了在所有地区和年份训练的模型的分类结果。然而，当模型转移到未知年份或未用于训练的地区时，SAR 数据提高了检测精度，而天气数据则降低了检测精度。所有年份都经过训练的模型，但并非所有研究地点都能检测到割草事件，准确度高达 F1 = 76%。对所有地区但并非所有年份进行训练的模型都检测到未训练年份的割草事件，其中 F1 高达 80%。
- **关键词**：Sentinel-1 Sentinel-2 Landsat 8 SVM 随机森林 CNN LSTM 反向散射 干涉相干 CAP
- **结论**：这篇论文的主要结论是，通过使用卫星光学和SAR时间序列数据以及深度学习模型（CNN和LSTM），成功实现了对整个生长季节的草地刈割事件的可靠检测。这些模型在准确性方面表现出色，即使在训练数据集之外的地区和年份也能够实现高精度的刈割事件检测。具体而言：  
1. CNN和LSTM模型都被证明在不同的条件下表现良好，LSTM在已知的研究地点和年份上表现稍微更好，而CNN在可迁移性方面表现更出色。  
2. 令人鼓舞的是，这些模型可以高精度地检测到生长季节内的第一次刈割事件，这对于欧洲和德国的农业和环境政策中的草地监测任务具有重要意义。  
3. 在德国进行时间序列分析时，研究发现不一定需要使用高级的间隙填充方法，如线性插值或随机森林间隙填充，因为这些方法对结果的影响较小，这有助于节省处理时间和计算资源。  
4. 特征选择方面存在一定的复杂性，光学数据对于已知的研究地点和年份更有优势，而包括光学和SAR数据在可迁移模型中取得了有利的结果。然而，当将天气数据引入可迁移模型时，需要谨慎考虑，因为它可能会降低模型在未知地点或年份上的性能。  
5. 针对欧洲农业政策的监测任务，研究建议使用CNN模型，结合光学和SAR数据，但不包括天气数据。然而，作者也指出，这些建议需要更多的研究来得出更具决定性的结论。  

### 研究背景
- **大背景**：本文的大背景涉及到遥感技术在草地监测领域的应用，特别是在欧洲和德国的农业和环境政策中。草地是农业生产和生态系统中的重要组成部分，因此需要对其进行监测和管理，以确保农业可持续性和环境保护。在这一大背景下，遥感技术提供了一种有效的工具，可以追踪草地的变化情况，例如刈割事件。
- **小背景**：文章关注了草地监测中的一个关键问题，即如何准确地检测刈割事件，特别是在整个生长季节内。
为了解决这个问题，文章使用了卫星光学和SAR（Synthetic Aperture Radar）时间序列数据，这些数据具有高时空分辨率，适合用于监测地表变化。
为了实现刈割事件的自动检测，文章采用了深度学习模型，包括CNN（Convolutional Neural Network）和LSTM（Long Short-Term Memory）模型。这些模型在图像和时间序列数据处理方面表现出色。
小背景还涉及到了研究的地理范围，即德国的草地，以及研究的具体目标，例如检测刈割事件的准确性和可迁移性。  

### 研究内容、成果
- **内容**：本文的研究内容主要集中在草地监测，特别是针对刈割事件的自动检测。具体包括以下方面：

1. 数据来源：文章使用了卫星时间序列数据，包括光学数据（如Landsat 8）和合成孔径雷达（SAR）数据（可能是Sentinel-1），这些数据提供了高时空分辨率的地表信息。  
2. 研究地点：研究集中在德国的草地，这是欧洲农业和环境政策的关键区域之一。  
3. 研究问题：主要研究问题是如何使用深度学习模型来准确检测刈割事件，以实现草地监测的自动化。  
4. 模型选择：研究使用了卷积神经网络（CNN）和长短时记忆网络（LSTM）等深度学习模型，这些模型被应用于卫星时间序列数据。  
5. 特征选择：文章还探讨了用于刈割事件检测的不同特征组合，包括光学数据、SAR数据以及天气数据。
   
- **成果**：文章的结果总结了对刈割事件检测的各种方法和特征组合的性能。以下是一些主要的研究结果：

1. 模型性能：CNN和LSTM模型在刈割事件检测中表现出了高准确性，即使在训练数据集未包括的地区和年份中也能取得良好的效果。LSTM模型在已知研究地点和年份上表现稍微更好，但CNN模型在可迁移性方面表现更优越。  
2. 第一次刈割事件检测：文章指出，这些模型可以高精度地检测到第一次刈割事件，这对于欧洲和德国农业和环境政策中的草地监测任务非常重要。  
3. 缺失数据处理：研究发现，在德国使用Landsat 8和Sentinel 2图像时，不需要使用复杂的缺失数据处理方法（如线性插值或随机森林填充），因为它们的影响很小。这节省了处理时间和计算资源。  
4. 特征选择：文章强调特征选择的重要性，并指出在已知的时间和空间范围内，光学数据对于表现优越，而光学和SAR数据的组合在可迁移模型上表现良好。此外，天气数据在已知研究地点和年份上对刈割事件分类起着重要作用，但在可迁移模型中需要谨慎使用，因为可能降低其在未知地点或年份上的性能。  

### 总结
- Conclusion by Thy:
1. 深度学习模型在时序SAR图像处理中的应用：该论文使用了深度学习模型（CNN和LSTM）来处理卫星时间序列数据，包括SAR数据。这可以提供一个参考框架，尤其是在探索如何使用深度学习来处理和分析时序SAR图像时。  
2. 特征选择：论文中强调了特征选择的重要性，并讨论了光学数据和SAR数据的组合。这可以启发考虑如何选择和组合时序SAR图像的特征以获得更好的性能。可以探索不同的特征组合，以确定哪些特征对于具体任务最有效。  
3. 缺失数据处理：论文提到，在使用卫星时间序列数据时，不一定需要复杂的缺失数据处理方法。这对于处理时序SAR图像中的可能出现的缺失数据情况也可能具有参考价值。可以考虑不同的方法来处理时序数据中的缺失或损坏的SAR图像。  
4. 刈割事件检测的可迁移性：论文中讨论了模型在不同地点和年份的可迁移性。这也与研究相关，因为时序SAR图像的处理可能需要在不同的地理位置和时间段中进行，了解模型的可迁移性对于研究非常重要。

