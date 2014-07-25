Title: 如何使用Xcode6创建Category文件
Date: 2014-07-03 00:08

愉快地用Xcode6写代码的时候发现，beta版的Xcode6居然把Category从新建向导里删除了，于是现在在Xcode6里新建Category文件有两个方法：
* 方法一：自己手动建Category文件。
* 方法二：导入Xcode5的设置。在命令行执行

```
cp -r /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Templates/File\ Templates/Cocoa\ Touch/Objective-C\ category.xctemplate /Applications/Xcode6-Beta.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Templates/File\ Templates/Source/
```
再重启Xcode6。你将会发现熟悉的Category出现在新建向导里啦。