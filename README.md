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
1. 网上有关显卡驱动的安装方法五花八门，建议先用最简单的办法安装（几行命令完事），不行再尝试别的路子。
```
ubuntu-drivers devices
```
此时会出现多个驱动，选择安装后缀写着“recommended”版本，比如我是```sudo apt install nvidia-driver-535```
```
sudo apt install nvidia-driver-XXX
```
2. 重启电脑后输入命令。
```
nvidia-smi
```

如果正确显示驱动信息，则证明安装成功。如果报错，再重启一遍。如果还不行，那就再想办法吧，大概率要卸载驱动重装。

3. 重启电脑如果黑屏并且左上角有个下划线形状的光标一直在跳，那就参考这个链接[https://blog.csdn.net/qq_43460315/article/details/142643949](https://blog.csdn.net/qq_43460315/article/details/142643949)。只要能回到图形界面，就可以重装显卡驱动了。
4. 然后装cuda。```nvidia-smi```命令显示的是当前显卡驱动适配的最高版本cuda，实际安装时再倒退一两个版本以求稳定。
   1. cuda装完之后添加环境变量可以直接写到```~/.bashrc```当中。
   2. 参考以下链接中的cuda和cudnn部分，pytorch先不要装。[https://blog.csdn.net/m0_55127902/article/details/135677560](https://blog.csdn.net/m0_55127902/article/details/135677560)
5. 最后装cudnn。同样参考上述链接。

### 关闭ubuntu内核自动更新以及显卡驱动自动更新
[https://blog.csdn.net/sdbyp/article/details/139606901](https://blog.csdn.net/sdbyp/article/details/139606901)  
[https://www.zhihu.com/question/617290612](https://www.zhihu.com/question/617290612)  
[https://www.cnblogs.com/schips/p/disable_ubuntu_kernel_autoupdate.html](https://www.cnblogs.com/schips/p/disable_ubuntu_kernel_autoupdate.html)

### 浏览器
1. ubuntu自带的火狐并不好用。如果在windows用的是edge或者chrome的话，在ubuntu中与windows同步即可。登录账号之后还能通用收藏夹等等，比较方便。安装方法随便一搜即可。
2. 安装完成后设置ubuntu默认浏览器，参考[https://cn.linux-console.net/?p=14822](https://cn.linux-console.net/?p=14822)

### qq
QQ有官方Linux版本，很好用，可惜工作相关内容都在微信上。Ubuntu的各种微信除了不能用的就是垃圾。
[https://blog.csdn.net/weixin_56656559/article/details/135640700](https://blog.csdn.net/weixin_56656559/article/details/135640700)

### 微信
