title: RobotFramework插件不支持动态库
author: cheng
date: 2018-04-13 14:40:25
tags:
---
##### 说明
	robot framework plugin for idea 还不支持动态库关键字.(2018-04-12)
    Selenium 3.0以后都不支持关键自动补全.
    PyCharm和idea还提示错误,无话可说.

<img src="/images/pasted-1.png" width="50%" height="50%">


##### 英文说明

	The issue is clearly related to the fact that SeleniumLibrary 3+ is dynamic library.
	
	In case of dynamic library, keywords are resolved during test execution (you can compare S2E 1.8 and SE 3+ code). Both this RobotFramework Support plugins work only with static libraries.
	
	If you want to use this plugin together with RF3+ with up to date keyword list, I would recommend you to use workaround (though it's dirty naughty hack), generating static library referencing keywords from dynamic one. So you can use it in your Robot resources or tests.