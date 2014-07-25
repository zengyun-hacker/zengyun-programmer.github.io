Title: 将CocoaPods替换成国内镜像
Date: 2014-07-11 13:44

每次执行`pod install`的时候，总会因为各种各样~~你懂得~~的原因要等半天。如果替换成国内镜像，能极大减少pod命令操作的时间。

### [step 1]备份原有的master仓库
进入~/.cocoapods/repos目录，复制原有的master文件夹，重命名为`master_backup`。

### [step 2]加入国内镜像
执行

```
pod repo remove master
pod repo add master http://git.oschina.net/akuandev/Specs.git
pod repo update
```

完成这两步后，我们的pod仓库已经更新为国内镜像了。