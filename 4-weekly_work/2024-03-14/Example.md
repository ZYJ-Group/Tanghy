# 组会 3.14
## [去雾域适应算法  ](https://github.com/HUSTSYJ/DA_dahazing)
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/d387ba8d-4bc7-492a-884f-cb3cfafbc29e)  
域适应框架，它由两个主要部分组成：图像翻译网络GS→R和GR→S，以及两个去雾网络GS和GR。图像翻译网络将图像从一个域翻译到另一个域，以弥合它们之间的差距。然后，去雾网络使用翻译图像和源图像（例如，合成图像或真实图像）执行图像去雾。  
如图所示，所提出的模型采用真实模糊图像 xr 和合成图像 xs 及其相应的深度图像 ds 作为输入。我们首先得到对应的平移图像 xs→r = GS→R(xs, ds)和 xr→s = GR→S(xr) 使用两个图像转换器。然后，我们将xs和xr→s传递给GS，xr和xr→s传递给GR来执行图像去雾。  

## 论文调研  
