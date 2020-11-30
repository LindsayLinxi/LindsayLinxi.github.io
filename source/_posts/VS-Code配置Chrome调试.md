---
title: VS Code配置Chrome调试
date: 2020-10-31 17:18:23
tags: '工具'
image: /images/theme/article_image_1.jpg
---
## 1.安装Debugger for Chrome插件

{% asset_img img_1.png This is an example image %}

More info: [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)

## 2.配置launch.json文件

{% asset_img img_2.png This is an example image %}

*launch.json配置*

{% asset_img img_3.png This is an example image %}

***注意*** *："request": "launch"每次都会以一个新用户的身份打开Chrome，无法使用已安装的Chrome拓展插件, 用"request": "attach"启动Chrome的远程调试，才能使用扩展程序*

## 3.启动Chrome远程调试
***Windows***
*1.右键单击Chrome快捷方式，然后选择属性*
*2.在“目标”字段中，附加 --remote-debugging-port=9222*
*3.或者在命令提示符下执行 /chrome.exe --remote-debugging-port=9222*

***Mac***
*在终端中执行 /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222*


***Linux***
*在终端中启动 google-chrome --remote-debugging-port=9222*

用"request": "attach"配置launch.json文件
{% asset_img img_4.png This is an example image %}

More info: [vscode-chrome-debug](https://github.com/Microsoft/vscode-chrome-debug/)