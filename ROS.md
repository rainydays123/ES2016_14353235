#ROS的配置
-----
###一、软件中心设置
- 检查安装环境

![](http://i.imgur.com/q35hmq0.png)

- apt加入新的源
- 
	$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

- 设置秘钥:
- 
	$ sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116

###二、安装ROS
- 确保系统软件处于最新版
- 
	$ sudo apt-get update

- 安装对应ROS版本
- 
	$sudo apt-get install libgl1-mesa-dev-lts-utopic
	$sudo apt-get install ros-jade-desktop-full
	$sudo apt-get install ros-jade-desktop
	$ sudo apt-get install ros-jade-ros-base
	sudo apt-get install ros-jade-PACKAGE
	sudo apt-get install ros-jade-slam-gmapping
	

- 可以通过下面命令查看使用包
- 

	$ apt-cache search ros-jade

###三、安装ROS
- 初始化ros
- 
	$ sudo rosdep init
	$ rosdep update

- 初始化环境变量
- 
	$ echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
	$ source ~/.bashrc

- 安装一个常用的插件
- 
	$ sudo apt-get install python-rosinstal

- 安装第三方插件
- 
	$apt-get source ros-jade-laser-pipeline

###三、安装测试
- 运行roscore命令

![](http://i.imgur.com/b0X6uoF.png)

######代表安装成功。

	