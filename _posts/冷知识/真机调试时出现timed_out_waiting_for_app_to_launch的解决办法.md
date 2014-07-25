# 真机调试时出现Timed out waiting for app to launch的解决办法
Date: 2013-08-30 11:36
Tags: 冷知识,iOS,真机调试

出现这种情况时请检查一下调试时使用的`Profile`文件，当使用adhoc的Profile进行真机调试时，debug会弹出`Timed out waiting for app to launch`错误，更换成`develop` Profile即可解决。