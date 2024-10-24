# ubuntu20.04环境配置
包括了ubuntu使用所需的基础环境配置，以及unitree_ros、Isaacgym等的安装。  

本文档没有对各个软件或包的安装过程进行重写排版，而是给出了可用的参考链接，然后对链接中有错误或需要补充的内容做单独标注。建议**先看补充内容**，再参考链接中的方法进行操作。参考格式如下：  
### 软件或包的名称
对以下链接内容的补充更正。

```
This is how you code.
```

 [参考安装方法的链接地址](https://github.com/MSP-xEN/ubuntu20.04)。

---

### 设置镜像源
1. 个人认为不需要备份原文件，把原来的内容注释掉即可。
2. 个人认为```vim```不好用，可用```gedit```代替，编辑完后记得保存。
3. 此后下载任何一个软件前，可能都需要在终端执行以下命令：
```
sudo apt update
```
4. 注意区别```sudo apt upgrade```命令。此命令会把所有可以升级的软件都升级，**然后可能就崩了，啥也用不了了**。

[https://blog.csdn.net/MacWx/article/details/137689898](https://blog.csdn.net/MacWx/article/details/137689898)。

### gcc, g++, make
```
sudo apt install build-essential
```

### VLC播放器
```
sudo apt install vlc
```

### nvidia显卡驱动+cuda+cudnn

