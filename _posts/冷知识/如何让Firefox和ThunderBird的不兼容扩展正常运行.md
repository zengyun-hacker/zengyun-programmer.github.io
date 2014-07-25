Title: 如何让Firefox和ThunderBird的不兼容扩展正常运行

Date: 2011-11-17 10:43:07

URL: /2011/11/17/%e5%a6%82%e4%bd%95%e8%ae%a9firefox%e5%92%8cthunderbird%e7%9a%84%e4%b8%8d%e5%85%bc%e5%ae%b9%e6%89%a9%e5%b1%95%e6%ad%a3%e5%b8%b8%e8%bf%90%e8%a1%8c/

FF使用了快速更新策略之后，版本是噌噌地往上升。且不说这策略是好是坏，FF升级的如此快，插件开发者可未必跟的这么快，所以我只能眼睁睁看着无数插件一个个接连因为不兼容而阵亡。

今天将ThunderBird重装后，发现平时赖以生存的几个插件也不幸牺牲。无奈动了DIY的精神，手动强制修改插件版本号，让插件都蒙混过关通过检查。

方法如下：

找到C:\Documents and Settings\%username%\Application Data\Thunderbird\Profiles\%当前profile名%\extensions中找到不兼容的插件，双击插件的xpi文件或者文件夹，用记事本其中的install.rdf文件打开，把em:maxVersion属性修改为8.*（改成大于8的数字也可以），保存后重启软件即可。

以上方法适用于Firefox和ThunderBird的插件。