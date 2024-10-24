# ubuntu20.04环境配置
包括了ubuntu使用所需的基础环境配置，以及unitree_ros、Isaacgym等的安装。  

本文档没有对各个软件或包的安装过程进行重写排版，而是给出了可用的参考链接，然后对链接中有错误或需要补充的内容做单独标注。建议**先看补充内容**，再参考链接中的方法进行操作。参考格式如下：  
### 软件或包的名称——用途
对以下链接内容的补充更正。

```
This is how you code.
```

 [参考安装方法的链接地址](https://github.com/MSP-xEN/ubuntu20.04)。

---

### 设置镜像源——下载更快
1. 个人认为不需要备份原文件，把原来的内容注释掉即可。
2. 个人认为```vim```不好用，可用```gedit```代替，编辑完后记得保存。
3. 此后下载任何一个软件前，可能都需要在终端执行以下命令：
```
sudo apt update
```
4. 注意区别```sudo apt upgrade```命令。此命令会把所有可以升级的软件都升级，**然后可能就崩了，啥也用不了了**。

[https://blog.csdn.net/MacWx/article/details/137689898](https://blog.csdn.net/MacWx/article/details/137689898)。

### gcc, g++, make——基本
```
sudo apt install build-essential
```

### VLC播放器——看视频的
```
sudo apt install vlc
```

### nvidia显卡驱动+cuda+cudnn——机器学习
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

### 关闭ubuntu内核自动更新以及显卡驱动自动更新——不然哪一天系统又崩了
[https://blog.csdn.net/sdbyp/article/details/139606901](https://blog.csdn.net/sdbyp/article/details/139606901)  
[https://www.zhihu.com/question/617290612](https://www.zhihu.com/question/617290612)  
[https://www.cnblogs.com/schips/p/disable_ubuntu_kernel_autoupdate.html](https://www.cnblogs.com/schips/p/disable_ubuntu_kernel_autoupdate.html)

### 浏览器
1. ubuntu自带的火狐并不好用。如果在windows用的是edge或者chrome的话，在ubuntu中与windows同步即可。登录账号之后还能通用收藏夹等等，比较方便。安装方法随便一搜即可。
2. 安装完成后设置ubuntu默认浏览器，参考[https://cn.linux-console.net/?p=14822](https://cn.linux-console.net/?p=14822)

### QQ
QQ有官方Linux版本，很好用，可惜工作相关内容都在微信上。Ubuntu的各种微信除了不能用的就是垃圾。
[https://blog.csdn.net/weixin_56656559/article/details/135640700](https://blog.csdn.net/weixin_56656559/article/details/135640700)

### 微信
1. 微信目前找到能用的只剩下优麒麟与腾讯合作开发的Linux原生微信[https://ubuntukylin.com/applications/106-cn.html](https://ubuntukylin.com/applications/106-cn.html)。
2. 功能只有发文字表情微信，连图片都发不了。优麒麟还有几个其他版本的微信，但在Ubuntu上似乎都用不了。还有个deep-in wine版本的微信没用过，不知道好用不。

### 搜狗输入法
参考以下链接[https://www.zhihu.com/tardis/zm/art/615309698?source_id=1005](https://www.zhihu.com/tardis/zm/art/615309698?source_id=1005)

### teamviewer——远程控制
1. 安装教程随便搜。
2. 可以设置固定密码，同时设置开机自动启动。参考以下链接[https://jingyan.baidu.com/article/0a52e3f4fee8a4bf62ed7230.html](https://jingyan.baidu.com/article/0a52e3f4fee8a4bf62ed7230.html)

### Clash——魔法
1. 先从以下链接下载解压。[https://jbox.sjtu.edu.cn/l/X1iUcn](https://jbox.sjtu.edu.cn/l/X1iUcn)
2. 创建快捷方式，收藏桌面到左侧栏。
   1. 命令行进入桌面，创建快捷方式。
   ```
   cd ~/桌面
   sudo gedit clash.desktop
   ```
   2. 然后将下面内容复制进去。Name即快捷方式图标下面显示的名称，Comment是这个快捷方式的文件名，Exec是可执行文件的所在路径（注意该路径中不要出现空格），Icon是快捷方式图标的所在路径（网上搜一个clash图标的图片文件）。
   ```
   [Desktop Entry]
   Version=1.0
   Name=Clash for Linux
   GenericName=Clash for Linux
   Comment=clash
   Exec=/home/david/Clash-for-Windows-0.20.20-x64-linux/cfw
   Icon=/home/david/Clash-for-Windows-0.20.20-x64-linux/icon.jpeg
   Terminal=false
   Type=Application
   Categories=Development;IDE;
   ```
   
   3. 赋予文件可执行权限。
   ```
   sudo chmod 744 clash.desktop
   sudo chmod +x clash.desktop
   ```

   4. 最后将此快捷方式复制到指定位置
   ```
   sudo cp clash.desktop /usr/share/applications
   ```

   此时点击桌面左下角的“显示应用程序”，应能找到Clash图标，并收藏到左侧栏。
3. 创建系统网络代理切换快捷键。
   1. 创建脚本，可以将此类快捷键脚本都存放到统一路径下。
   ```
   mkdir ~/keyboard_shortcut
   gedit ~/keyboard_shortcut/toggle_proxy.sh
   ```

   2. 在脚本文件中写入以下内容，保存。
   ```
   #!/bin/bash
   export DISPLAY=:0
   export XAUTHORITY=/run/user/$(id -u)/gdm/Xauthority
   
   PROXY_MODE=$(gsettings get org.gnome.system.proxy mode)
   
   
   if [ "$PROXY_MODE" == "'none'" ]; then
       gsettings set org.gnome.system.proxy mode 'manual'
       echo "代理已切换为手动"
   else
       gsettings set org.gnome.system.proxy mode 'none'
       echo "代理已禁用"
   fi
   ```

   3. 赋予脚本可执行权限。
   ```
   chmod +x ~/keyboard_shortcut/toggle_proxy.sh
   ```
   4. 打开设置-设备-键盘-拉到最下方-自定义快捷键+，填写相关内容。其中在命令一栏输入脚本所在路径```/home/david/keyboard_shortcut/toggle_proxy.sh```，保存。

### zotero+相关插件——文献阅读和管理
1. 我装的zotero6，听说7不太好用。参考以下链接[https://jingyan.baidu.com/article/0a52e3f4fee8a4bf62ed7230.html](https://jingyan.baidu.com/article/0a52e3f4fee8a4bf62ed7230.html)
2. 插件不用装太多，我装了翻译、汉化、笔记、风格共四个热门插件，然后浏览器再装一个插件用来导入文献。插件商店链接[https://zotero-chinese.com/plugins/](https://zotero-chinese.com/plugins/)。插件安装教程自行搜索即可。

### git+ssh配置+git代理设置——github
[https://blog.csdn.net/qq_31635851/article/details/123333398](https://blog.csdn.net/qq_31635851/article/details/123333398)  
[https://blog.csdn.net/qq_31635851/article/details/123333398](https://blog.csdn.net/qq_31635851/article/details/123333398)

### vscode
网上随便搜个教程即可。记得用学生身份搞一个github copilot，参考以下链接[https://docs.github.com/zh/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-your-copilot-subscription/getting-free-access-to-copilot-as-a-student-teacher-or-maintainer](https://docs.github.com/zh/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-your-copilot-subscription/getting-free-access-to-copilot-as-a-student-teacher-or-maintainer)

### ros
1. 记得先装ros再装anaconda，不然可能会有问题。
2. 如果安装或使用ros时提示“cmake版本过低”，不能直接重装cmake（卸载cmake会把ros一起卸载），而是要上网搜索更改软链接的方法。
3. 参考以下链接[https://blog.csdn.net/qq_44339029/article/details/108919545](https://blog.csdn.net/qq_44339029/article/details/108919545)

### gazebo
随便搜教程。

### 宇树

### isaacgym
