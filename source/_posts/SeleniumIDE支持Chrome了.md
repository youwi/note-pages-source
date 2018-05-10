title: SeleniumIDE支持Chrome了
author: cheng
tags: []
categories:
  - robot framework
date: 2018-04-20 13:27:00
---
SeleniumIDE悄悄支持Chrome了.从源代码来看使用react做了重新开发

(2018-04-20)
<img src="/images/pasted-4.png" style="width:600px;border:solid 1px" >

##### 四不像的脚本
selenium-ide以前生成的脚本是浏览器无关的纯文本.
像这种:
```
|click |button| 
|type  |input |abc|
```
也支持导出为html(旧版本支持)
现在索性直接用json文件保存了...
还专程做了一个项目sideex,没什么人气:
http://sideex.org

注:脚本为.side文件,连v1和v2为同一个类型

<img src="/images/pasted-5.png" style="width:400;border:solid 1px" >

生成的脚本其实并没有什么用
  - 脚本不能用来共享(套件和用例多人一起分工)
  - 脚本不能用来协作(如放到git)
  - 实际可用性不如robot framwork 
  - 导出的代码还要改来改去,各种不如意
  - 缺少keywords管理(Action共享)
  
总的说来,这玩意只能做做登陆登陆登陆登陆登陆

##### 期待功能:
 - 协作
 - 拆分用例
 - keyword管理