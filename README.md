# manjaro个人使用配置

#### 软件仓库配置

- ###### 切换国内软件源

  ```bash
  sudo pacman-mirrors -c China -i
  sudo pacman-mirrors -g
  #更新系统到最新
  sudo pacman -Syyu
  ```

  

- ###### 添加archlinuxcn软件源码

  ```bash
  #安装vim
  sudo pacman -S vim
  #修改pacman配置文件
  sudo vim /etc/pacman.conf 
  #末行添加下面内容
  [archlinuxcn]
  Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
  
  #更新系统
  sudo pacman-mirrors -g
  sudo pacman -Syyu
  #安装archlinuxcn-keyring
  sudo pacman -S archlinuxcn-keyring
  ```

- ###### 启动AUR仓库

  ```bash
  sudo pacman -S --needed base-devel
  sudo pacman -S git yay
  ```

### 安装英伟达专有驱动(非NV用户请跳过)

#### so nvidia fxxk you！！！

- ###### 卸载开源video驱动

```bash
sudo manjaro-settings-manager
#选择video-linux右键移除
```

![](/home/axooly/图片/Screenshot_20230105_142810.png)

![](/home/axooly/图片/Screenshot_20230105_142351.png)

- ###### 安装Nvidia video驱动

  ```bash
  #安装中途切勿重启或关机
  sudo manjaro-settings-manager
  #选择其中一个右键安装
  ```

  ![](/home/axooly/图片/Screenshot_20230105_142810.png)

  ![image-20230105142734506](/home/axooly/.config/Typora/typora-user-images/image-20230105142734506.png)

- ###### 安装依赖 载入模块

  ```bash
  sudo pacman -S linux61-headers acpi_call-dkms xorg-xrandr xf86-video-intel
  #linux61-headers 需要改成你使用的内核版本
  sudo modprobe acpi_call
  ```

- ###### 安装显卡切换

  ```bash
  git clone https://github.com/dglt1/optimus-switch-sddm.git
  cd ~/optimus-switch-sddm
  chmod +x install.sh
  sudo ./install.sh
  #切换核显
  sudo set-intel.sh 
  #切换独显
  sudo set-nvidia.sh
  #结束重启电脑
  ```

### 安装中文输入法

- ###### 安装fcitx5

  ```bash
  sudo pacman -S fcitx5  fcitx5-configtool   fcitx5-qt fcitx5-chinese-addons
  #安装词库
  yay -S fcitx5-pinyin-zhwiki
  ```

- ###### 启用fcitx5输入法（仅manjaro系统）

  ```bash
  sudo pacman -S manjaro-asian-input-support-fcitx5
  #安装完成后重启电脑
  ```

### 简易美化KDE桌面(个人习惯风格配置勿喷！！)

#### 最终效果

![image-20230105155543991](/home/axooly/.config/Typora/typora-user-images/image-20230105155543991.png)

![image-20230105155623782](/home/axooly/.config/Typora/typora-user-images/image-20230105155623782.png)

![image-20230105155712288](/home/axooly/.config/Typora/typora-user-images/image-20230105155712288.png)

![image-20230105155740181](/home/axooly/.config/Typora/typora-user-images/image-20230105155740181.png)

#### 安装ocs-url（方便安装主题）

```bash
yay -S ocs-url
```

#### 安装全局主题

```bash
#主题地址 https://store.kde.org/p/1325243
#安装全局主题建议重启
```

![image-20230105150053742](/home/axooly/.config/Typora/typora-user-images/image-20230105150053742.png)

![image-20230105150321608](/home/axooly/.config/Typora/typora-user-images/image-20230105150321608.png)

![image-20230105150354941](/home/axooly/.config/Typora/typora-user-images/image-20230105150354941.png)

![image-20230105150430430](/home/axooly/.config/Typora/typora-user-images/image-20230105150430430.png)

**打开系统设置->外观->全局主题**

![image-20230105150605645](/home/axooly/.config/Typora/typora-user-images/image-20230105150605645.png)

![image-20230105150745009](/home/axooly/.config/Typora/typora-user-images/image-20230105150745009.png)

![image-20230105150819332](/home/axooly/.config/Typora/typora-user-images/image-20230105150819332.png)

![image-20230105150847533](/home/axooly/.config/Typora/typora-user-images/image-20230105150847533.png)

#### 安装图标

```
#项目地址 https://github.com/PapirusDevelopmentTeam/papirus-icon-theme
yay -S papirus-icon-theme-git 
```

![image-20230105152242793](/home/axooly/.config/Typora/typora-user-images/image-20230105152242793.png)

#### 毛玻璃效果

```bash
sudo pacman -S devilspie 
mkdir ~/.devilspie
vim ~/.devilspie/kde.ds
#配置文件添加下面内容
```

```lua
(if (or
                (is (window_class) "systemsettings")
                (is (window_class) "dolphin")
                (is (window_class) "konsole")
                (is (window_class) "ksysguard")
                (is (window_class) "discover")
                (is (window_class) "kinfocenter")
                (is (window_class) "kwalletmanager5")
                (is (window_class) "ark")
                (is (window_class) "kwrite")
                (is (window_class) "spectacle")
                (is (window_class) "lattedock")
                (is (window_class) "kwin")
                (is (window_class) "Code")
                (is (window_class) "okular")
        )
        (begin
                (spawn_async (str "xprop -id " (window_xid) " -f _KDE_NET_WM_BLUR_BEHIND_REGION 32c -set _KDE_NET_WM_BLUR_BEHIND_REGION 0 "))
                (spawn_async (str "xprop -id " (window_xid) " -f _NET_WM_WINDOW_OPACITY 32c -set _NET_WM_WINDOW_OPACITY 0xdfffffff"))
        )
)
```

```bash
#需要添加窗口执行下面命令选择需要的窗口,不需要添加请忽略
xprop | grep 'CLASS'
#示例
xprop | grep 'CLASS'
#输出WM_CLASS(STRING) = "typora", "Typora" 最后""内的就是CLASS值
vim vim ~/.devilspie/kde.ds#在(is (window_class) "okular")后面添加下面内容CLASS值自己修改
(is (window_class) "Typora")
```

```bash
#配置devilspie自启动
cat >> ~/.autostart.sh << EOF
#!/bin/bash
devilspie -a&
EOF
chmod +x ~/.autostart.sh
sudo vim /etc/systemd/system/autostart.service 
[Unit]
Description=run shell script

[Service]
ExecStart= /home/用户名/autostart.sh
Type = simple

[Install]
WantedBy=multi-user.target


#执行命令
sudo systemctl daemon-reload
sudo systemctl enable autostart.service 
sudo systemctl start autostart.service 
```

