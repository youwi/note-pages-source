title: 理清几个webdriver的关系
author: cheng
date: 2018-04-18 14:06:11
tags:
---
#### 平常用到的driver

| driver   |      port     |  path |
|----------|:-------------:|------:|
| chromedriver |  9515 | / |
| geckerdriver |  4444   | /   |
| safaridriver |  0 |   / |
| iedriverserver | ? |  /  |
| StandaloneServer| 4444| /wd/hub |

他们都可以做为独立远程服务器执行--负责创建浏览器/关闭浏览器,各有用途.
也可以做为本地服务启动.
使用w3c webdriver协议(https://www.w3.org/TR/webdriver/)

平常调试代码时,chromedriver启动是隐性透明的.

#### 示例
以chrome为例:
```
new ChromeDriver()//竟然是运行chromedriver.exe
```
![upload successful](/images/pasted-3.png)

#### 启动速度太慢的问题
后面有时间我再写点.目前主要是因为driver创建了一个浏览器副本.
- java我已经解决了
- python还在做