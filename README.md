# ubuntu20.04环境配置
包括了ubuntu使用所需的基础环境配置，以及unitree_ros、Isaacgym等的安装。  

本文档没有对各个软件或包的安装过程进行重写排版，而是给出了可用的参考链接，然后对链接中有错误或需要补充的内容做单独标注。建议**先看补充内容**，再参考链接中的方法进行操作。如果针对同一内容给出了多个参考链接，大概是需要对各个链接内容取并集。参考格式如下：  
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
5. 参考链接[https://blog.csdn.net/MacWx/article/details/137689898](https://blog.csdn.net/MacWx/article/details/137689898)。

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
   此时会出现多个驱动，选择安装后缀写着“recommended”版本（但是版本也不要太高，我是4060配535版本就挺好）；不能装带server的，那是服务器版本。
   ```
   sudo apt install nvidia-driver-XXX
   ```

   比如我是```sudo apt install nvidia-driver-535```。

   如果是50系显卡，“软件与更新”中不存在推荐驱动，上述命令也不生效。需要去官网下载对应的.run文件（5060下的是570.run）。很多教程说要禁用图形界面，但实测应该不需要禁用。直接执行以下命令
   ```
   sudo chmod  a+x NVIDIA-Linux-x86_64-396.18.run
   sudo ./NVIDIA-Linux-x86_64-396.18.run -no-x-check -no-nouveau-check -no-opengl-files
   ```
   然后在安装过程中需要选择nvidia property还是GPL，选GPL，参考以下链接[https://minetest.top/archives/zai-linuxxia-wei-nvidia-50xi-an-zhuang-xian-qia-qu-dong](https://minetest.top/archives/zai-linuxxia-wei-nvidia-50xi-an-zhuang-xian-qia-qu-dong)。还有个x config，选no。
3. 重启电脑后输入命令。
   ```
   nvidia-smi
   ```

如果正确显示驱动信息，则证明安装成功。如果报错，再重启一遍。如果还不行，那就再想办法吧，大概率要卸载驱动重装。

3. 重启电脑如果黑屏并且左上角有个下划线形状的光标一直在跳，那就参考这个链接[https://blog.csdn.net/qq_43460315/article/details/142643949](https://blog.csdn.net/qq_43460315/article/details/142643949)或者[https://zhuanlan.zhihu.com/p/608786007](https://zhuanlan.zhihu.com/p/608786007)。只要能回到图形界面，就可以重装显卡驱动了。
4. 然后装cuda。```nvidia-smi```命令显示的是当前显卡驱动适配的最高版本cuda，实际安装时再倒退一两个版本以求稳定。
   1. cuda装完之后添加环境变量可以直接写到```~/.bashrc```当中。
   2. 参考以下链接中的cuda和cudnn部分，pytorch先不要装。[https://blog.csdn.net/m0_55127902/article/details/135677560](https://blog.csdn.net/m0_55127902/article/details/135677560)
5. 最后装cudnn。同样参考上述链接。

### 关闭ubuntu内核自动更新以及显卡驱动自动更新——不然哪一天系统又崩了
[https://blog.csdn.net/sdbyp/article/details/139606901](https://blog.csdn.net/sdbyp/article/details/139606901)  
[https://www.zhihu.com/question/617290612](https://www.zhihu.com/question/617290612)  
[https://www.cnblogs.com/schips/p/disable_ubuntu_kernel_autoupdate.html](https://www.cnblogs.com/schips/p/disable_ubuntu_kernel_autoupdate.html)

如果要更新显卡驱动，需要解除掉禁止自动更新，参考下文[https://zhuanlan.zhihu.com/p/671274846](https://zhuanlan.zhihu.com/p/671274846)

### 浏览器
1. ubuntu自带的火狐并不好用。如果在windows用的是edge或者chrome的话，在ubuntu中与windows同步即可。登录账号之后还能通用收藏夹等等，比较方便。安装方法随便一搜即可。
2. 安装完成后设置ubuntu默认浏览器，参考[https://cn.linux-console.net/?p=14822](https://cn.linux-console.net/?p=14822)

### QQ
QQ有官方Linux版本，很好用。[https://blog.csdn.net/weixin_56656559/article/details/135640700](https://blog.csdn.net/weixin_56656559/article/details/135640700)

### 微信
Linux官方版本已更新。[https://linux.weixin.qq.com/](https://linux.weixin.qq.com/)。下载完毕后```sudo dpkg -i WeChatxxx```即可安装。

### 搜狗输入法
参考以下链接[https://www.zhihu.com/tardis/zm/art/615309698?source_id=1005](https://www.zhihu.com/tardis/zm/art/615309698?source_id=1005)

### teamviewer——远程控制
1. 安装教程随便搜。
2. 可以设置固定密码，同时设置开机自动启动。参考以下链接[https://jingyan.baidu.com/article/0a52e3f4fee8a4bf62ed7230.html](https://jingyan.baidu.com/article/0a52e3f4fee8a4bf62ed7230.html)

### Clash——魔法
#### 命令行安装法
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

#### 下载clash AppImage图形界面法
在这个链接下[https://github.com/clash-verge-rev/clash-verge-rev/releases/tag/v1.6.2](https://github.com/clash-verge-rev/clash-verge-rev/releases/tag/v1.6.2),AppImage版本然后设置执行权限直接执行

### zotero+相关插件——文献阅读和管理
1. 我装的zotero6，听说7不太好用。参考以下链接[https://jingyan.baidu.com/article/0a52e3f4fee8a4bf62ed7230.html](https://jingyan.baidu.com/article/0a52e3f4fee8a4bf62ed7230.html)
2. 插件不用装太多，我装了翻译、汉化、笔记、风格共四个热门插件，然后浏览器再装一个插件用来导入文献。插件商店链接[https://zotero-chinese.com/plugins/](https://zotero-chinese.com/plugins/)。插件安装教程自行搜索即可。

### git+ssh配置+git代理设置——github
[https://blog.csdn.net/qq_31635851/article/details/123333398](https://blog.csdn.net/qq_31635851/article/details/123333398)  
[https://zhuanlan.zhihu.com/p/378894743](https://zhuanlan.zhihu.com/p/378894743)

### vscode
1. 网上随便搜个教程即可。
2. 记得用学生身份搞一个github copilot，参考以下链接[https://docs.github.com/zh/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-your-copilot-subscription/getting-free-access-to-copilot-as-a-student-teacher-or-maintainer](https://docs.github.com/zh/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-your-copilot-subscription/getting-free-access-to-copilot-as-a-student-teacher-or-maintainer)
3. vscode自带debug，通过debug读懂项目文件和调试代码。[https://www.bilibili.com/video/BV1vDakeDE2n?vd_source=a724bfd1b4b642794a14a920e236e2f1&spm_id_from=333.788.videopod.episodes](https://www.bilibili.com/video/BV1vDakeDE2n?vd_source=a724bfd1b4b642794a14a920e236e2f1&spm_id_from=333.788.videopod.episodes)

### ros
#### fishros一键安装法
fishros 一键安装参考[https://blog.csdn.net/zyx201824101450/article/details/142767709](https://blog.csdn.net/zyx201824101450/article/details/142767709)
注意最好打开clash代理科学上网,ROS有一步需要梯子.

##### 自行安装法
1. 记得先装ros再装anaconda，不然可能会有问题。
2. 如果安装或使用ros时提示“cmake版本过低”，不能直接重装cmake（卸载cmake会把ros一起卸载），而是要上网搜索更改软链接的方法。
3. 参考以下链接[https://blog.csdn.net/qq_44339029/article/details/108919545](https://blog.csdn.net/qq_44339029/article/details/108919545)

### gazebo
随便搜教程。

### anaconda
1. 一定确保先装ros再装conda。
2. 不要默认启动conda。
3. 不要把conda加到环境变量中，用ubuntu20.04默认的python3就挺好。
4. 参考以下链接[https://blog.csdn.net/m0_50117360/article/details/108403586](https://blog.csdn.net/m0_50117360/article/details/108403586)
5. 如果conda还是莫名自动启动了，用以下命令禁止：
   ```
   conda config --set auto_activate_base false
   ```

### 宇树
1. LCM装1.5版本，不要装1.4版本。其余包与链接中保持一致即可。
2. 如果安装```unitree_legged_sdk```后试运行```./example_walk```报错```error while loading shared libraries: liblcm.so.1: cannot open shared object file: No such file or directory```，那么执行以下命令
   ```
   sudo apt install liblcm-dev
   ```
3. 知乎链接中的“4.修改环境变量”没必要。
4. 参考链接[https://icymon.github.io/IT_infrastructure/Ubuntu20.04Install_unitree_ros.html](https://icymon.github.io/IT_infrastructure/Ubuntu20.04Install_unitree_ros.html)  
   [https://zhuanlan.zhihu.com/p/543566158](https://zhuanlan.zhihu.com/p/543566158)
   
### isaacgym+leggedgym——强化学习训练
1. ubuntu20.04在安装isaacgym后需要修改环境变量。
   ```
   sudo gedit ~/.bashrc
   ```
   添加以下内容：
   ```
   export LD_LIBRARY_PATH=/home/david/anaconda3/envs/rlgpu/lib
   ```
   此后创建需要使用isaacgym的新环境时也需要如此操作。
2. numpy可能需要重装1.21版本。或者把np.float报错位置代码按提示修改即可。
   ```
   pip install numpy==1.21
   ```

3. setuptools可能需要回退版本。
   ```
   conda install setuptools=59.5.0
   ```
4. 其他可能出现的问题参见以下链接[https://blog.csdn.net/weixin_45315065/article/details/132902799](https://blog.csdn.net/weixin_45315065/article/details/132902799)
5. isaacgym和leggedgym安装参考以下链接（如果只装isaacgym就停在相应步骤即可）[https://github.com/leggedrobotics/legged_gym](https://github.com/leggedrobotics/legged_gym)
6. 导入宇树模型进leggedgym。
   1. 克隆以下项目[https://github.com/unitreerobotics/unitree_rl_gym](https://github.com/unitreerobotics/unitree_rl_gym)，将```unitree_rl_gym/resources/robots/go2```整个文件夹复制到```legged_gym/resources/robots```
   2. 将```unitree_rl_gym/legged_gym/envs/go2```整个文件夹复制到```legged_gym/legged_gym/envs```。
   3. 在```legged_gym/legged_gym/envs/__init__.py```文件中，仿照```a1```机器人的相关语句格式，注册```go2```（共需添加两行代码）。
  
### Issaclab安装
`wget -O install_isaaclab.sh https://docs.robotsfan.com/install_isaaclab.sh && bash install_isaaclab.sh`

使用该一键安装指令，选择1.4.1即可


#### 选择项

**Conda Environment Creation**

如果之前没有会自动创建，然后会一键安装所需的库

**Do you want to launch graphical interfacen for vertification**

这个地方如果是20.04或者ros非humble及以上，**选择n**，不然会无法完成接下来的安装

**Choose where to clone**

选个路径放issaclab的代码，随便选就好

**Pull the latest changes**

选择最新的

**Verifiy with graphical interface**

这里可以打开看看了，一般第一次加载会非常缓慢，大概要十分钟左右，如果看到force quit选wait。也可以在issaclab文件夹里 python scripts/tutorails/00_sim/create_empty.py, 如果正常打开就是安装成功了
