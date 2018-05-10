title: 远程服务器上安装无界面Chrome
author: cheng
date: 2018-04-23 13:32:54
tags:
---
远程服务器上安装无界面Chrome,用的阿里云服务器.

- ssh登陆
- centos7 
- shell only(没有图形界面)

其实开源的早就准备OK的.
	
    yum install chromedriver.x86_64
    yum install chromium-headless
    
    # 安装完成以后可以找到它:
    # rpm -ql chromium-headless
    # /usr/lib64/chromium-browser/headless_shell
    # 注不要用官方chromedriver
  
运行方式很特别:
	
    /usr/lib64/chromium-browser/headless_shell --no-sandbox  --headless --remote-debugging-port=9222 --disable-gpu
    
注:用root启动有警告


|     |     |     |
|-----|-----|-----| 
|text1|text2|text3|
|text1|text2|text3|


