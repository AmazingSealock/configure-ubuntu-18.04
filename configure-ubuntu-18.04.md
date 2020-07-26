### Hades Canyon Configuration

Copyright © 2018 FortiSTray_Action. All Rights Reserved.

---
#### How to install ubuntu alongside Windows
##### Refer to this article to assign disks
https://blog.csdn.net/lxlong89940101/article/details/80604937        
https://blog.csdn.net/baidu_36602427/article/details/86548203

#### Preparation before installing libraries

##### Change Ubuntu source to tuna(更改下载源，这里是使用的清华镜像站的源)

```bash
sudo gedit /etc/apt/sources.list
```

Replace all contains to follows

```bash
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse

```

```bash
sudo apt-get update && sudo apt-get upgrade 
```

##### Install Git

```bash
sudo apt-get install git
```

##### Install CMake

```bash
sudo apt-get install cmake
```

#### Install librealsense (v2.16.1)（ubuntu16.04，2.24以下的realsense版本可以参照这个）

* Download source code from Github (Release > Intel® RealSense™ SDK 2.0 (build 2.16.1))

  Extract the `.tar.gz` file to `~/Library`

  Unplug any connected Intel RealSense camera

* Navigate to librealsense root directory

  ```bash
  sudo apt-get install libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev
  sudo apt-get install libglfw3-dev
  sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/ 
  sudo udevadm control --reload-rules && udevadm trigger
  ./scripts/patch-realsense-ubuntu-lts.sh
  echo 'hid_sensor_custom' | sudo tee -a /etc/modules
  mkdir build && cd build
  cmake .. -DCMAKE_BUILD_TYPE=Release
  sudo make uninstall && make clean && make -j8 && sudo make install
  ```
  
 #### Install librealsense (v2.16.1)（16.04，2.24一下的realsense版本可以参照这个）
 参照官方教程：https://github.com/IntelRealSense/librealsense/blob/master/doc/distribution_linux.md
 
 检查linux内核版本
 ```bash
  uname -a
  ```
 如果不是4.16或者5.0版本可能会出现连接不上深度相机的情况
  

#### Install PCL (v1.8.1)

* Download source code from Github (Release > pcl-1.8.1)

  Extract the `.tar.gz` file to `~/Library`

* Navigate to PCL root directory

  ```bash
  sudo apt install libboost-all-dev libeigen3-dev libflann-dev libvtk6-dev
  sudo apt install libproj-dev
  mkdir build && cd build
  cmake -DCMAKE_BUILD_TYPE=Release ..
  make -j8
  sudo make -j8 install
  ```

#### Install OpenCV (v3.4.4) with OpenCV_Contrib (v3.4.4)

- Download OpenCV source code from Github (Release > OpenCV 3.4.4)

  Download OpenCV_Contrib source code from Github (Release > 3.4.4)

  Extract the `.tar.gz` file to `~/Library`

  Copy OpenCV_Contrib folder into OpenCV folder and rename it as `opencv_contrib`

- Navigate to OpenCV root directory

  ```bash
  sudo apt-get install build-essential
  sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
  mkdir build && cd build
  cmake -DCMAKE_BUILD_TYPE=Release ..
  make -j8
  sudo make install
  ```

#### Work environment optimization

##### Install chromium

```bash
sudo apt-get install chromium-browser
```

##### Install Sogou Pinyin input method（适用于16.04版本）

Download `.deb` file from official website

```bash
sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb
sudo apt-get install -f
```

Set `System Settings > Language Support > Keyboard input method system = fcitx`

Log out &  Log in

Keyboard icon on the right top > add `Sogou Pinyin`

```bash
sudo apt-get remove fcitx-ui-qimpanel
```

Log out &  Log in

Ubuntu18.04请参考
https://blog.csdn.net/qq_33159059/article/details/85019467

##### Install vscode

Download `.deb` file from official website

```bash
sudo apt-get install -f
sudo dpkg -i code_1.29.1-1542309157_amd64.deb
```
##### Resolve dependencies
```bash
sudo apt-get install -f
```




