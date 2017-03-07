---
title: HTML4 和 HTML5 的10个关键区别
date: 2017-03-07 00:33:14
tags: github 创建分支
---
[http://blog.csdn.net/guang11cheng/article/details/37757201](http://note.youdao.com/)
[http://blog.csdn.net/top_code/article/details/51931916](http://note.youdao.com/)
[http://www.cnblogs.com/horanly/p/6265182.html
](http://note.youdao.com/)

在github上创建仓库：
`Create a new repository on the command line`

```
touch README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/BrentHuang/MyRepo.git
git push -u origin master
```

在本地新建一个分支： `git branch Branch1`  
切换到你的新分支: `git checkout Branch1`  
将新分支发布在github上： `git push origin Branch1`  
在本地删除一个分支： `git branch -d Branch1`  
在github远程端删除一个分支： `git push origin :Branch1`  
(分支名前的冒号代表删除)

直接使用git pull和git push的设置
```
Git branch --set-upstream-to=origin/master master 
git branch --set-upstream-to=origin/ThirdParty ThirdParty
git config --global push.default matching
```
