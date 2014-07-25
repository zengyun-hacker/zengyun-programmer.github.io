Title: Linux运行级别

Date: 2011-08-13 13:23:33

URL: /2011/08/13/linux%e8%bf%90%e8%a1%8c%e7%ba%a7%e5%88%ab/

运行级别表示系统当前运行的模式，类似与windows的正常模式，安全模式。

Linux一般分为一下几个运行级别

0 Halt the system

1 Single user mode

2 Basic multi user mode

3 Multi user mode

5 Multi user mode with GUI

6 Reboot the system

S, s Single user mode 

在终端输入$ /sbin/runlevel 可以查询当前运行级别，屏幕会输出两个数字 如  2 5

表示上一个运行级别是2，当前运行级别是5