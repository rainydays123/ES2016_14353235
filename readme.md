#第一次实验报告
![Mou icon](http://25.io/mou/Mou_128.png)
##DOL框架
![](http://i.imgur.com/oRuncM2.png)
##DOL配置过程
* 安装必要环境
	$	sudo apt-get update<br>
	$	sudo apt-get install ant<br>
	$ 	sudo apt-get install openjdk-7-jdk<br>
	$	sudo apt-get install unzip<br>
* 下载文件
* 解压文件
	$	mkdir dol<br>
	$	unzip dol_ethz.zip -d dol<br>
	$	tar -zxvf systemc-2.3.1.tgz<br>
* 编译systemc
	$	cd systemc-2.3.1<br>
	$	mkdir objdir
	$	cd objdir
	$	../configure CXX=g++ --disable-async-updates
* 编译dol
	$	sudo make install<br>
	$	cd ../dol<br>
* 替换路径：<br>
	property name="systemc.inc" value="YYY/include"<br>
	property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"<br><br>
	$	ant -f build_zip.xml all 
##实验体会
DOL全称distribute operate layer,是开发并行式软件的程序框架。
	
