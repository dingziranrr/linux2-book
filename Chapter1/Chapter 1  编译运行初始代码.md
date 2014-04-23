# Chapter 1  编译运行初始代码

##安装Git
打开终端，输入
~~~
sudo apt-get install git
~~~
等待安装完成

##下载初始代码
在想要存放代码的位置输入
~~~
git clone https://github.com/dingziranrr/linux2
~~~
等下载完成，进入此目录
~~~
cd linux2
~~~
##编译代码
输入
~~~
make
~~~
##运行代码
在此终端，以后称为终端A，输入
~~~
./job
~~~
打开另一个终端，以后称为终端B，进入同样目录，输入
~~~
./enq Demo
~~~
之后可在终端B输入以下命令随时查看Demo的运行状态
~~~
./stat
~~~
最终运行结果如下图
[![Screen](https://raw.github.com/dingziranrr/linux2-book/master/1.jpg)](https://raw.github.com/dingziranrr/linux2-book/master/1.jpg)
