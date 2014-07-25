Title: 升级Mac自带的git
Date: 2014-07-16 14:22

不知不觉git已经到1.9.0了，而Mac自带的git仍在1.8.5。实在忍不住围观一下git升级的新特性，于是下决心琢磨如何在Mac上升级。

#### [step 1]卸载掉原有的git  
首先看看原来的git的安装位置
在shell中执行  
```
which git
```
唔。能发现我的git装在`/usr/local/bin`中。执行
```
mv /usr/bin/git /usr/bin/git_backup
```
将原来的git文件夹备份起来。

#### [step 2]使用brew安装新的git
```
brew install git
```
我在执行这句话的时候遇到brew link时提示`Permission denied - /usr/local/lib/perl5`。原因是brew没有访问`/usr/local`文件夹的权限。执行
```
sudo chown -R `whoami` /usr/local
```
可以为local文件夹增加写的权限。权限成功添加之后再执行
```
brew link git
```
在命令行打入`git --version`试试，可以看到git已经成功安装啦，并且版本号是最新的1.9.0。

#### [step 3]删除原有的git目录。
记得第一步备份了之前的git目录嘛？新的git安装成功之后，可以淡定地删除之前备份的那个目录了。执行
```
rm -rf /usr/bin/git_backup
```
git更新就完成啦。