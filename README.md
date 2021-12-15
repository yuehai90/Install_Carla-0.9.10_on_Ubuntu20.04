# Install_Carla-0.9.10_on_Ubuntu20.04
Carla officially gave two different installation schemes, one for quick installation and the other for complete construction. If you just want to simulate various models of autonomous driving, then quick installation is the best choice. As for the complete construction of Carla, it can unlock lower-level functions. In theory, it allows very personalized modeling of everything in the Carla virtual world. If it is a company or team engaged in autonomous driving related fields, it needs to install the complete construction of Carla. The following content is based on the quick installation package guide given by the official Carla and a summary of its own installation experience.


**本文以中文书写，英文翻译为谷歌翻译，如有不准确请见谅**


Carla官方给出了两种不同的安装方案，一种为快速安装，另一种为完整构建。如果仅仅是想对自动驾驶的各种模型进行仿真，那么快速安装便是最好的选择。至于Carla的完整构建则可以解锁更底层的功能，理论上讲它允许对Carla虚拟世界中的万事万物进行非常个性化的建模。如果是从事自动驾驶相关领域的企业或团队需要安装Carla的完整构建。
> 以下内容依据Carla官方给出的快速安装包指南并结合自身安装经验总结。

* [Before you begin](#before-you-begin)  
  
* [Install amdgpu pro](#install-amdgpu-pro)  
    
* [Install and Upgrade Python3](#install-and-upgrade-python3)
  
* [Download and run Carla](#download-and-run-carla)
* [Before you begin](#before-you-begin)
* [Before you begin](#before-you-begin)
------

Before you begin
------

- 以下为我自己的硬件配置，其中比较关键是显卡型号。因为不同显卡型号涉及到不同的显卡驱动的安装。如果你的电脑配备了其他型号的显卡（比如Nidia），那么请查看其他的相关安装说明。但是无论如何请满足官方文档中给出的硬件最低配置要求，即至少6GB显存的显卡以及至少20GB的空余硬盘空间。其他的要求详见官方指南。
    
|组件|型号|
|----|-----|
|CPU|Intel® Core™ i5-10500 CPU @ 3.10GHz × 12|
|graphics|AMD® Radeon RTX 6600 8G|
|RAM|16GB|
|Memory|1TB|
|System|Ubuntu 20.04.3 LTS|
|GNOME|3.36.8|
  

**此外，以下的安装过程适用于完全全新的Ubuntu20.04系统，即刚刚安装好Ubuntu系统的电脑。因此，一个假设是Ubuntu系统中并未配置任何关于Carla或者Python3.7的依赖项。如果你已经安装过类似的依赖项，那么请参考以下过程并适当作出调整。请注意，每一台电脑或者每一个系统根据使用者及其使用目的的不同一般来说都是不同的，而不同的配置往往造成安装过程的差异。**

Install amdgpu pro
------
- 下载官方提供的包文件
- 解压缩
- 查看系统是否已识别显卡
- 查看系统是否已安装驱动
- 安装驱动并重启
- 重启后黑屏问题


Install and Upgrade Python3
------
- 升级
- 配置依赖项
- 下载python3.7包，解压并进入
- 配置
- 编译并安装
- 创建软连接
- 安装并更新pip3.7
- 添加pygame numpy

Download and run Carla
------
- 下载carla包并移动到文件夹，在主目录下，也可以自行安排位置
- 解压缩
- 运行carla
- 用python3.7打开示例

