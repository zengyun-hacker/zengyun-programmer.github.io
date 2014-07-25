# Xcode 编译选项详解（一）

Date: 2013-07-11 23:11  
Tags: 冷知识,iOS,编译选项  

>以下所有编译选项都基于Xcode 4.6。本文基于Apple Xcode文档、《Professional Xcode 3》、以及Google搜索结果翻译而成。我对于编译认识较浅。如有解释不当的地方请谅解。在某些翻译可能会不恰当的地方，都附上了英文原文。

## Architectures 架构

### Additional SDKs
在编译的时候需要附加的SDK。
### Architectures
支持的处理器架构。不同的处理器对应不同版本的iPhone。  

```
其中支持Armv6的设备为：  

* iPhone1   
* iPhone3G  
* iPod Touch 1  
* iPod Touch 2  
```
```
支持Armv7的设备为：

* iPhone 3GS  
* iPhone 4  
* iPad   
* The New iPad  
* iPod Touch 3G  
* iPod Touch 4  
```
```
支持Armv7s的设备为：  
* iPhone5 
``` 
iPhone对于指令集是向下兼容的。高版本的iPhone可以运行低版本的指令集。因此要适应全系列的iPhone，Architectures应选择Armv6。  
### Base SDK
这决定了你的app所能支持的iOS最高版本。如果你选择了iOS6.1，则你的app只能被iOS 6.1.X以下的系统安装。Xcode默认设置为能够支持的最新版本。  
### Build Active Architecture Only
如果此项为YES，则在Xcode会根据设备的版本只将相应的Architecture编译入app。如连接了iPhone4进行编译，Build Active Architecture Only为YES，则编译时只会构建Armv7的二进制文件。若连接的是iPhone5，则构建出Armv7s的二进制文件。  
这个选项在Debug时默认为YES，在Release时默认为NO。这使得Debug时编译的时间比Release快，更加方便调试。  
### Supported Platforms
app所支持的平台，有iOS和OSX两个选项。
### Valid Architectures
app预期将要应用到的架构。默认与Architectures的值相同。这个选项让你可以在编译的时候只打包Armv7s架构，但是兼容Armv6,Armv7。  
## Build Locations
### Build Products Path  
产品文件和编译中间文件的根目录。产品文件和编译时临时文件都将放在这个目录的子目录中。  
### Intermediate Build Files Path  
编译时临时文件的存放位置。编译中间文件格式为product name+.build，如MyProduct.build。  
### Per-configuration Build Product Path  
Directory path. Identifies the directory that holds temporary files for the active build configuration.  
当前编译设置下的产品存放位置。  
### Per-configuration Intermediate File Path
Directory path. Identifies the directory that holds temporary files for the active build configuration.  
当前编译设置下编译时临时文件的存放位置。  
### Precompiled Headers Cache Path
Directory path. Specifies the directory in which to place precompiled headers. Targets can share precompiled headers by specifying the same value for this build setting.  
存放预编译头文件的位置。通过这个配置，Targets可以互相共享预编译的头文件。  
## Build Options
### Build Variants
Space-separated list of identifiers. Specifies the binary variants of the product. You can create additional variant names for special purposes. For example, you can use the name of a build configuration as a variant name to create highly customized binaries.  
Values:  
normal: Use to produce a normal binary.  
profile: Use to produce a binary that generates profile information.  
debug: Use to produce a binary with debug symbols, additional assertions, and diagnostic code.  
此项可以设定生成产品的变种。您可以创建额外的产品变种作为特殊用途。例如，您可以使用编译配置文件的名称来创建一个高度定制的二进制文件。  

```
Build Variants的值有三个：
normal-用于生成普通的二进制文件
profile-用于可以生成配置信息的二进制文件
debug-用于生成带有debug标志、额外断言和诊断代码的二进制文件
```
### Compiler for C/C++/Object-C
选择使用的编译器。Xcode自带有两种选项，Apple LLVM和LLVM GCC。建议使用默认选项---Apple LLVM。  
### Debug Information Format
这个选项决定了记录debug信息的文件格式。选项有DWARF with dSYM File和DWARF。建议选择DWARF with dSYM File。DWARF是较老的文件格式，会在编译时将debug信息写在执行文件中。   
### Generate Profiling Code
是否生成配置代码。默认选择NO。  
### Precompiled Header Uses Files From Build Directory
预编译build路径中的头文件。由于编译过程比较耗时，且两次编译之间未必会改动所有文件。因此将不会改动的常用文件保留成预编译文件将大大减少编译时的时间。建议这一项选择YES。  
### Run Static Analyzer
运行静态分析器。  
### Scan All Source Files for Includes
扫描include文件所包含的所有源文件。  
### Validate Built Product
这个选项决定了是否在编译的时候进行验证。验证的内容和app store的审查内容一致。默认选项是debug时不验证，release时验证，这样就保证了每个release版本都会通过validate，让被拒的风险在提交app store之前就暴露出来，减少损失。   

```
注意：
1. 这个选项只在连接真机的时候有效。在使用模拟器时无效。不过我用真机试了一下，似乎也没有检查出代码里的私有API。
2. 想手动validate，可以在Organizer->Archives里找到需要检查的Archive，点击Validate按钮即可。这样检查似乎靠谱些，可以查出私有API等违规操作。
```