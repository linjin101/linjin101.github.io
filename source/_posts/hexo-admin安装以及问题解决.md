title: hexo-admin安装以及问题解决
categories:
  - hexo
tags:
  - hexo-admin
  - github
author: linjin101
date: 2017-03-13 00:09:00
---
#### 1.安装hexo和创建一个博客  
```
npm install -g hexo
cd ~/
hexo init my-blog
cd my-blog
npm install
```

#### 2.安装hexo-admin和本地运行
```
npm install --save hexo-admin
hexo server -d
open http://localhost:4000/admin/
```
**<font color=red>(hexo-admin管理只能在本地用,github上面只有静态页面不能进行管理,切记!!!)</font>**  



#### 3.密码保护
如果你的hexo-admin需要一些保护密码，你只需要添加一些你的hexo配置变量到配置文件_config.yml：
```
admin:
  username: myfavoritename
  password_hash: be121740bf988b2225a313fa1f107ca1
  secret: a secret something
```

#### 4.安装问题处理
```
$ npm install --save hexo-admin
npm WARN deprecated minimatch@2.0.10: Please update to minimatch 3.0.2 or higher to avoid a RegExp DoS issue
hexo-site@0.0.0 E:\git\linjin101.github.io

npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.0.0 (node_modules\chokidar\node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.1.1: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})
```

#### 5.解决
```
npm install minimatch@"3.0.2"  
npm update -d
```

如果还有问题:  
升级后依旧报错,只好重装:

```
npm update minimatch
npm -v minimatch
npm install -g npm@3
```

清理,生成,本地启动
```
hexo clean && hexo g && hexo s
```   

浏览器打开
http://localhost:4000/admin/

![image](/images/20170313091240.png)

#### 6.NPM介绍:  
是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：  
允许用户从NPM服务器下载别人编写的第三方包到本地使用。  
允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。  
允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。   


