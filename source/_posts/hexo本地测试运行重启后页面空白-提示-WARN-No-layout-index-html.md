---
title: 'hexo本地测试运行重启后页面空白,提示 : WARN No layout: index.html'
date: 2017-03-07 12:44:35
categories:
- hexo
tags:
- hexo空白
- hexo本地测试
---
运行git clone 指令获得主题后（假设是NEXT主题），在theme主题下保存文件夹的名称为：hexo-theme-next-0.4.0  
那么如果在config里设置的是next，就会出现这样的WARN，http://localhost:4000/  
显示的是空白。只要把theme下的文件夹名称改为next就显示正常了.要么就是获取的样式文件夹是空的,需要重新下载.