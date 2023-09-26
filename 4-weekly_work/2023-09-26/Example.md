# UNet复现（大方向/篇数）
**失败经历**  
更换数据库，但是报错，现在猜测原因是标签值的变化。    
原先的数据集跑出来INFO: Unique mask values: [0, 1]  
现在的数据集跑出来INFO: Unique mask values: [0, 1, 2, 3, 4, 5, 6]  

报错：  
![2023-09-26-02](https://github.com/ZYJ-Group/Tanghy/assets/94824386/af079a8f-aab7-4eb1-92ea-fb9f638c5bbf)  

ps.[源码](https://github.com/milesial/Pytorch-UNet)  
