# IDEA

## 快捷键

* ctrl+D：复制当前行
* ctrl+Y：删除当前行
* alt+/：自动补全
* 自动格式化：ctrl+alt+L
* 自动运行：shift+f10
* 自动生成构造器：alt+insert 或右键点击
* 查看类的继承关系：ctrl+H
* 跳转到方法：ctrl+B

* 自动导入：Setting->Editor->General->Auto Import
* 大小写匹配：Setting->Editor -> General -> Code Completion->Match case
* 自动命名：加`.var`

## 模板代码

​	设置：Setting->Editor->live templates

* main
* fori：for循环
* sout

## 查看源码

* 要求在IDEA中对源码进行了配置（默认安装后应该是自动配置好的）。
* 右键方法，选择`Go To`，选择`Declaration or Usages`。快捷键：`ctrl+B`

## 断点调试

* 断点调试中，对象以运行类型执行。

* 断点可以提前下，也可以在Debug过程中动态下断点。

* 快捷键：
  * F7 Step Into:跳入方法体。
  * F8 Step Osver:跳过，逐行执行，不进入方法体。
  * shift+F8 Step Out:跳出方法体。
  * F9:继续，执行到下一个断点。

* 在IDEA调试中进入源码：

  * 使用Force step into跳入源码。

  * 对IDEA进行配置：

    1. 进入`Setting->Build,Execution,Deployment->Debugger->Stepping`。

    2. Do not step into the classes中，取消勾选`ajva.*`,`javax.*`。