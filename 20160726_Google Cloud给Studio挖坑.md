# Google Cloud给Studio挖坑

> 2016.07.26

## 前言

最近遇到一个奇怪的现象，用Android Studio默认的ApplicationTest的时候，只要一运行Test方法，Studio就会卡住不动，要过好久才能恢复运行。（只是界面卡住，什么都不能点，软件随时可以关闭）

今天卸载了然后重新安装，然并卵啊，难道是2.1.2的bug？

## 其实是Google Cloud的锅

今天再次运行Test的时候，Studio弹了一个错误提示（右上角红色字体弹窗），我突然想到干嘛不看下Event Log。

看到如下日志，一直在尝试检索可用的Cloud设备，这里的Cloud就是Google Cloud。

```
11:05:26 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:05:46 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:06:06 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:06:26 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:06:46 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:07:06 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:07:26 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:07:46 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:08:06 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:08:26 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:08:46 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:09:06 Failed to retrieve available cloud devices! Please try again later. Details (show balloon)
11:09:06 : Typeahead request blocked: Time: 240859
```

之前我写过一篇日志，因为Sock代理的原因，Google Cloud无法正常登陆，这个bug要之后的版本才能修复。但是呢，Google Cloud SDK在安装并初始化成功后，Android Studio会自动登陆用于初始化的Cloud账号，而一跑Test就不知道什么鬼的去检索什么云设备，一直检索不到就卡住了。。。

## 解决方法

方法一：直接卸载Google Cloud SDK。（我不想卸载，以后还准备用呢）<br>
方法二：在Android Studio中退出已登录的账号。（简单易行，哈哈）

Mark：以后遇到问题多看日志
