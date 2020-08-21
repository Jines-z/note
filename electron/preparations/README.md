## 安装 Electron 之前需要做的准备

1、首先确定你准备安装的 `electron` 的版本号；

2、打开 [https://npm.taobao.org/mirrors/electron](https://github.com/jines-z/rn-mobx-starter) 下载对应版本的 zip 文件，例如 `electron-v9.2.1-win32-x64.zip`；

3、将下载好的 zip 文件放到 `C:\Users\zheng\AppData\Local\electron\Cache\` 目录下；

4、打开 cmd 执行以下命令：
``` 
设置全局下载源：（非必须）
npm config set registry https://npm.taobao.org/mirrors/node

设置node源码加速：
npm config set disturl https://npm.taobao.org/mirrors/node  

将 electron 包下载地址注册为淘宝的镜像：
npm config set ELECTRON_MIRROR https://npm.taobao.org/mirrors/electron/
```

5、在 `C:\Users\zheng\AppData\Local\electron\Cache\` 目录下新建文件夹 `httpsnpm.taobao.orgmirrorselectronv9.2.1electron-v9.2.1-win32-x64.zip`，将 zip 文件再复制一份到新建好的文件夹中；

接下来，就可以愉快的 `npm install electron` 和 `npm install electron-builder` 了~

[目录](https://github.com/jines-z/note)
