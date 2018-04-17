title: RobotFramework插件强制支持动态库
author: cheng
date: 2018-04-16 14:46:11
tags:
---
## 起因
对于SeleniumLibrary 3.0 全是动态关键字.原生插件不支持动态关键字索引.

由于pycharm一直报错很不爽,fork了代码https://github.com/youwi/intellibot
可以从这里直接下载jar包来安装.暂不打算合并代码.

效果:
![upload successful](/images/pasted-2.png)

说下idea的索引结构,调用索引有以下方法:

	PyFunctionNameIndex.find() 返回方法
	PyModuleNameIndex.find()   返回文件
	PyClassNameIndex.find()    返回类
    层级关系:
    Module->Class->Functions
    故(伪码):
    PyModuleNameIndex.find(?)
    	->t.getChildren()
        ->t.isPyClass
        ->t.getNextSibling()  //获取兄弟文件
        ->t.getChildren() 
        ->t.isPyClass
        ....

```java

 // com.millennialmedia.intellibot.psi.element.HeadingImpl.java
  /* 
     * search sibling library by keywords
     * patch for SeleniumLibrary dynamic keywords
     * support all libraries that contain "keywords" package.
     * @param files  all pyClass
     * @param libraryName  default search is keywords.
     */
    void findChildrenClass(Collection files,String libraryName){
//        // this is temporary patch,each patch return All keywords from file
        // Force Patch by Selenium
//        String[] sourcelist = {
//                "open_browser",
//                "get_cookies",
//                "input_text_into_prompt",
//                "get_webelement",
//                "submit_form",
//                "select_frame",
//                "execute_javascript",
//                "register_keyword_to_run_on_failure",
//                "set_screenshot_directory",
//                "get_list_items",
//                "get_table_cell",
//                "wait_for_condition",
//                "active_drivers",
//                "create_driver",
//                "select_window"
//        };
//        for (String str : sourcelist) {
//            Collection<PyFunction> funcs = PyFunctionNameIndex.find(str, getProject());
//            for (PyFunction pyfunc : funcs) {
//                PyClass cs = pyfunc.getContainingClass();
//                files.add(new RobotPythonClass(cs.getName(), cs, ImportType.LIBRARY));
//            }
//        }
        Collection<PyFile> fileList=PyModuleNameIndex.find(libraryName,getProject(),true);
        for(PyFile pyFile:fileList){
            PyFile nextFile=pyFile;

            while (nextFile!=null){
                PsiElement[] all= nextFile.getChildren();
                for(PsiElement psiElement:all){
                    if(psiElement instanceof PyClass){
                        files.add(new RobotPythonClass(((PyClass) psiElement).getName(), (PyClass) psiElement, ImportType.LIBRARY));
                    }
                }
                nextFile= (PyFile) nextFile.getNextSibling();
            }
        }
    }

```