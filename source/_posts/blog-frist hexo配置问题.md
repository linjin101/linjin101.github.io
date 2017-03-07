---
title: blog-frist hexo配置问题
date: 2017-03-07 00:33:14
categories:
- hexo
tags: 
- hexo配置问题
---
[https://www.zhihu.com/question/38219432](http://note.youdao.com/)

贴上一篇我之前搭建博客时，参考的教程
引用自：Xuanwo's Blog// 史上最详细的Hexo博客搭建图文教程 
-----------------------------------
配置Deployment首先，你需要为自己配置身份信息，打开命令行，然后输入：
git config --global user.name "yourname"
git config --global user.email "youremail"
同样在_config.yml文件中，找到Deployment，然后按照如下修改：
deploy:
type: git
repo: git@github.com:yourname/yourname.github.io.git
branch: master
如果使用git方式进行部署，执行npm install hexo-deployer-git --save来安装所需的插件
然后在当前目录打开命令行，输入：
hexo d
随后按照提示，分别输入自己的Github账号用户名和密码，开始上传。
-------------------------------
你看看会不会是这边的配置出现了问题。


作者：孙武军
链接：https://www.zhihu.com/question/38219432/answer/75389052
来源：知乎
著作权归作者所有，转载请联系作者获得授权。

=======================================================

提交项目，部署

继续在本目录命令行  
安装部署工具（方便以后更新）  
`npm install hexo-deployer-git -save`  
1、初始化本地仓库：  
`git init`   
2、连接远程仓库：  
如果是第一次使用git，在使用git的时候会提示输入用户名和密码，用户名是自己的注册邮箱。  
`git remote add origin https://github.com/wapchief/wapchief.github.io.git`    
3、发布hexo到github page  
`hexo clean && hexo g && hexo d`  
4、添加文件到本地仓库  
`git add`  
5、提交声明
`git commit -m '内容'`  
6、推送到远程仓库（github）
`git push origin`  
这里建议创建一个新的分支hexo，用于管理hexo文件。   提交的的时候只提交hexo网站html、css、等源文件。而默认的master用来部署更新项目,具体可以看我的github地址分支情况https://github.com/wapchief/wapchief.github.io
创建并切换到新建分支：
git checkout -b hexo
将分支推送到远程仓库：
git push origin hexo
这时打开网站就能看到效果了。
记得提交以后去github上把hexo分支设置默认，以后写文章等都要部署。
文章在hexo目录下的\source_posts文件夹中，是md格式，也就是Markdown格式。
以后可以用以下命令部署。也就是第三步

//等于一次性执行了，清空、刷新、部署三个命令  
`hexo clean && hexo g && hexo d`  
如果部署时不clean，可能之前修改的文章还存在。包括一些配置等，有时候部署完成后并没有改变，其实是缓存未清除。


