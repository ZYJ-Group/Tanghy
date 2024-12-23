# UNet复现 and GEEmap（大方向/篇数）
### UNet  
**出现的问题**
在服务器中运行的时候，无法import datasets里面的py文件。（但是可以import 类似的utils里面的py文件）
![2023-09-20-02](https://github.com/ZYJ-Group/Tanghy/assets/94824386/13230cdd-ebad-4204-9023-6b5b404fa5af)  
（ps.处理一个下午仍然未果）

### 安装GEEmap
**出现的问题**
1. 使用conda下载的时候，下载速度过慢，使用pip稍快。  
2. 安装好后，无法打开Jupyter notebook。  
![2023-09-20-03](https://github.com/ZYJ-Group/Tanghy/assets/94824386/613b8778-c001-44b2-8c30-133fc152149c)  
解决办法：  
pip uninstall Traitlets  
pip install Traitlets==5.9.0  
3. 使用Chrome浏览器打开jupyter notebook巨卡无比，改用firefox浏览器稍好一点点，但仍然很卡。
