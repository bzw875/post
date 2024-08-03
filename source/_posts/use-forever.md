---
title: 使用forever来持久运行node.js应用
date: 2022-03-30 12:36:12
updated: 2022-03-30 12:36:12
tags:
categories:
---


本网站不够稳定，经常莫名其妙的node.js进程退出，（相比之下java服务稳得像狗一样）然后不得不登录在启动服务；

## forever.js
[https://github.com/foreversd/forever](https://github.com/foreversd/forever)

所以我就使用forever.js来持久运行我的应用；

安装forever
```
npm install forever -g
```

进入项目文件中
```
forever start app.js
```

再说一下其他简单的命令
列出forever启动的应用
```
forever list
```
结束forever启动的应用
```
forever stop app.js
```

### 最后
别忘了使用nohup命令，
```
nohup forever start app.js &
```
exit 退出shell，不要点关闭按钮，否则用户的进程都会死掉的
```
exit
```