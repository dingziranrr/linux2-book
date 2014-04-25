# Chapter 2 了解JOB的工作流程
本章节通过在job中加入log信息来了解job的工作流程
##添加#define
打开job.c，在头部#include之后添加
~~~
#define DEBUG
~~~
##添加调试代码
在job.c的最下方的main方法中，在struct声明后，增加如下代码
~~~
#ifdef DEBUG
    printf("DEBUG is open!");
#endif
~~~
保存，使用make重新编译，然后运行./job，会发现出现调试信息
[![Screen](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/1.jpg)](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/1.jpg)
##捕捉时钟信号的触发
在main函数的之后的代码段，如图
[![Screen](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/2.jpg)](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/2.jpg)
setitimer函数每一秒发送一个SIGVTALRM信号，这个信号和SIGCHLD都被sig_handler函数捕捉，现在找到sig_handler函数
如图，sig变量表示接受的信号是什么信号，通过case语句针对不同信号执行不同操作
[![Screen](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/3.jpg)](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/3.jpg)
现在在case SIGVTALRM:下方增加如下代码
~~~
#ifdef DEBUG
    printf("SIGVTALRM received!\n");
#endif
~~~
重新编译运行程序，可以看到每秒打印一次
[![Screen](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/4.jpg)](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/4.jpg)
##scheduler函数
每一次捕捉SIGVTALRM信号，会执行一次scheduler函数，修改scheduler函数的第一个#ifdef DEBUG中的内容，改成如下,这里当每从fifo读取一次，就打印提示
[![Screen](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/5.jpg)](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/5.jpg)
scheduler函数之后的代码，改成如下
[![Screen](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/6.jpg)](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/6.jpg)
最后重新编译运行，可以看到job中每一秒的循环所做的事情
[![Screen](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/7.jpg)](https://raw.githubusercontent.com/dingziranrr/linux2-book/master/Chapter2/7.jpg)
