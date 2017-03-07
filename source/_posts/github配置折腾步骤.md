---
title: github配置折腾步骤
date: 2017-03-06 23:46:55
categories:
- hexo
tags: 
- github报错
---
win10安装报错,提示需要管理员账户.
后来修改权限半天,而且也切换管理员账户还是出错.误解搜索错误解决办法,最后替换淘宝的源解决问题.
报错:
```
$ npm install hexo-cli -g
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.0.0 (node_modules\hexo-cli\node_modules\chokidar\node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.1.1: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})
npm ERR! Windows_NT 10.0.14393
npm ERR! argv "D:\\nodejs\\node.exe" "D:\\nodejs\\node_modules\\npm\\bin\\npm-cli.js" "install" "hexo-cli" "-g"
npm ERR! node v6.10.0
npm ERR! npm  v3.10.10
npm ERR! path C:\Users\linjin101\AppData\Roaming\npm\node_modules\hexo-cli
npm ERR! code EPERM
npm ERR! errno -4048
npm ERR! syscall rename

npm ERR! Error: EPERM: operation not permitted, rename 'C:\Users\linjin101\AppData\Roaming\npm\node_modules\hexo-cli' -> 'C:\Users\linjin101\AppData\Roaming\npm\node_modules\.hexo-cli.DELETE'
npm ERR!     at moveAway (D:\nodejs\node_modules\npm\lib\install\action\finalize.js:38:5)
npm ERR!     at destStatted (D:\nodejs\node_modules\npm\lib\install\action\finalize.js:27:7)
npm ERR!     at D:\nodejs\node_modules\npm\node_modules\graceful-fs\polyfills.js:267:18
npm ERR!     at FSReqWrap.oncomplete (fs.js:123:15)
npm ERR!
npm ERR! Error: EPERM: operation not permitted, rename 'C:\Users\linjin101\AppData\Roaming\npm\node_modules\hexo-cli' -> 'C:\Users\linjin101\AppData\Roaming\npm\node_modules\.hexo-cli.DELETE'
npm ERR!     at Error (native)
npm ERR!  Error: EPERM: operation not permitted, rename 'C:\Users\linjin101\AppData\Roaming\npm\node_modules\hexo-cli' -> 'C:\Users\linjin101\AppData\Roaming\npm\node_modules\.hexo-cli.DELETE'
npm ERR!     at moveAway (D:\nodejs\node_modules\npm\lib\install\action\finalize.js:38:5)
npm ERR!     at destStatted (D:\nodejs\node_modules\npm\lib\install\action\finalize.js:27:7)
npm ERR!     at D:\nodejs\node_modules\npm\node_modules\graceful-fs\polyfills.js:267:18
npm ERR!     at FSReqWrap.oncomplete (fs.js:123:15)
npm ERR!
npm ERR! Error: EPERM: operation not permitted, rename 'C:\Users\linjin101\AppData\Roaming\npm\node_modules\hexo-cli' -> 'C:\Users\linjin101\AppData\Roaming\npm\node_modules\.hexo-cli.DELETE'
npm ERR!     at Error (native)
npm ERR!
npm ERR! Please try running this command again as root/Administrator.

npm ERR! Please include the following file with any support request:
npm ERR!     E:\git\hexo\npm-debug.log
```  

后来执行下面语句安装成功hexo  
``npm install -g hexo --registry=https://registry.npm.taobao.org``

淘宝 NPM 镜像  
[http://npm.taobao.org/](http://note.youdao.com/)  
镜像使用方法（三种办法任意一种都能解决问题，建议使用第三种，将配置写死，下次用的时候配置还在）:  

**1.通过config命令**  
npm config set registry https://registry.npm.taobao.org   
npm info underscore  
（如果上面配置正确这个命令会有字符串response）  

**2.命令行指定**  
npm --registry https://registry.npm.taobao.org info underscore   

**3.编辑 ~/.npmrc 加入下面内容**  
registry = https://registry.npm.taobao.org  












