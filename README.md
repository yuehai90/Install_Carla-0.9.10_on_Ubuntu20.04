# Install_Carla-0.9.10_on_Ubuntu20.04
Carla officially gave two different installation schemes, one for quick installation and the other for complete construction. If you just want to simulate various models of autonomous driving, then quick installation is the best choice. As for the complete construction of Carla, it can unlock lower-level functions. In theory, it allows very personalized modeling of everything in the Carla virtual world. If it is a company or team engaged in autonomous driving related fields, it needs to install the complete construction of Carla. The following content is based on the quick installation package guide given by the official Carla and a summary of its own installation experience.


Carla官方给出了两种不同的安装方案，一种为快速安装，另一种为完整构建。如果仅仅是想对自动驾驶的各种模型进行仿真，那么快速安装便是最好的选择。至于Carla的完整构建则可以解锁更底层的功能，理论上讲它允许对Carla虚拟世界中的万事万物进行非常个性化的建模。如果是从事自动驾驶相关领域的企业或团队需要安装Carla的完整构建。
> 以下内容依据Carla官方给出的快速安装包指南并结合自身安装经验总结。

* [Before you begin](#before-you-begin)  
  
* [Install amdgpu pro](#install-amdgpu-pro)  
    
* [Install and Upgrade Python3](#install-and-upgrade-python3)
  
* [Download and run Carla](#download-and-run-carla)

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
- 下载官方驱动，这里选择的版本是Radeon™ Software for Linux® 21.30 Release，是配系统为Ubuntu20.04.3

![pic](https://github.com/yuehai90/Install_Carla-0.9.10_on_Ubuntu20.04/blob/main/img/2021-12-15%2011-28-29%20amdpro%20download.png)

- 在下载位置解压缩，比如在/Downloads
```
tar -Jxvf amdgpu-pro-21.30-1290604-ubuntu-20.04.tar.xz
```


- 查看系统是否已识别显卡
```
lspci | grep -i vga
```
若系统已识别AMD显卡，则应该看到以下显示
![pic](https://github.com/yuehai90/Install_Carla-0.9.10_on_Ubuntu20.04/blob/main/img/2021-12-15%2012-00-54%20amd1.png)

- 查看系统是否已安装驱动
```
dpkg -l amdgpu-pro
```
应该看到未安装的信息


- 如果已经安装了其他版本的任何驱动，那么应该卸载。之后再次进入刚才解压缩的文件夹，并安装驱动
```
cd /Downloads/amdgpu-pro-21.30-1290604-ubuntu-20.04

sudo ./amdgpu-pro-install -y
```
等待安装完成并重启


- 重启后黑屏问题

许多用户报告在安装了amdgpu pro之后重启黑屏的故障。我本人在安装过程中未曾遇到。如果你遇到了类似问题请查阅相关解决方案。其次，大量解决方案指出解决重启黑屏问题需要卸载amdgpu pro驱动，并仅仅安装amdgpu驱动。**请注意，为了保证carla的正确运行，必须安装amdgpu pro驱动。**

Install and Upgrade Python3
------
- 升级并更新
```
sudo apt update

sudo apt upgrade
```

- 配置依赖项
```
sudo apt install build-essential make cmake -y
sudo apt install libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev -y
sudo apt-get install zlib1g-dev
```
**请注意，这一步十分重要。若在安装过程中报错并指出还需要安装其他的依赖项，那么请根据报错信息一步一步安装所有依赖项，直到最后全部安装成功。**


- 下载python3.7，解压并进入。我选择的版本为3.7.7，经过实测3.7.8也可以。
```
tar -zxvf Python-3.7.7.tgz

cd Python-3.7.7
```


- 配置
```
./configure --enable-optimizations
```


- 编译并安装,该过程也许会持续一段时间，根据电脑性能的不同。如果安装过程中报错，那么意味着之前的依赖项有未正确安装或者缺少依赖项。请确保所有依赖项都被正确安装。
```
sudo make
sudo make install
```


- 创建软连接

**为了不破坏Ubuntu20.04原生python3.8，必须对新安装的python3.7建立软连接**

在安装好python3.7之后，找到其安装位置，你应该可以在如下位置找到安装好的python3.7

![pic](https://github.com/yuehai90/Install_Carla-0.9.10_on_Ubuntu20.04/blob/main/img/2021-12-15%2013-43-38%20python3.7.png)

但如果你未在该文件夹内找到，可以使用搜索功能定位出安装位置。一般来说它总是会被安装在/usr/local中的某一个地方

**使用你电脑中安装好的python3.7的位置，并在/usr/bin中创建软连接。以下命令以我的安装位置为例**
```
sudo ln -s -f /usr/local/bin/python3.7/bin/python3.7 /usr/bin/python3.7
```


- 安装并更新pip3.7
在建立好软连接之后，可以通过在命令行输入python3.7而对其直接调用。调用python3.7安装对应的pip

```
sudo apt-get install python3.7-pip
```

之后以同样的方式对pip3.7创建软连接
```
sudo ln -s -f /usr/local/bin/python3.7/bin/pip3.7 /usr/bin/pip3.7
```


- 添加pygame numpy
最后，通过在命令行直接调用pip3.7，来对python3.7导入两个carla需要用到的库
```
pip3.7 install --user pygame numpy
```
至此，python3.7的环境搭建完成


Download and run Carla
------
- 下载carla包并移动到主目录下名为carla的（新创建）文件夹中。你也可以自行安排carla文件的位置。我使用的carla版本为0.9.10
![pic](https://github.com/yuehai90/Install_Carla-0.9.10_on_Ubuntu20.04/blob/main/img/2021-12-15%2014-01-02%20carla%20download.png)

- 找到你放置carla压缩包的位置并解压缩
```
tar -zxvf CARLA_0.9.10.tar.gz
```

- 运行carla以及python examples

当解压缩完成后，你应该能够看到CarlaUE4.sh，通过如下命令启动carla
```
./CarlaUE4.sh
```

至此，carla环境的搭建已完成。

**如果需要查看Carla中自带的PythonAPI中的示例，一定要通过python3.7调用，而不是pyghon3。以下是一个调用的例子**
```
cd PythonAPI/examples

python3.7 spawn_npc.py
```

**在运行任何通过PythonAPI调用的代码时，一定要保证CarlaUE4.sh的运行，不能够将其关闭而单独调用PythonAPI中的代码**

![pic](https://github.com/yuehai90/Install_Carla-0.9.10_on_Ubuntu20.04/blob/main/img/2021-12-15%2014-10-22%20carla%20run.png)

![pic](https://github.com/yuehai90/Install_Carla-0.9.10_on_Ubuntu20.04/blob/main/img/2021-12-15%2014-11-52%20carla%20run.png)
