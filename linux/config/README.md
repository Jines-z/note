## Linux 服务器配置教程

1、安装依赖包
```shell script
yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel unzip zip
```

2、下载并解压安装包
```shell script
cd /usr/local
wget http://nginx.org/download/nginx-1.18.0.tar.gz
tar -xvf nginx-1.18.0.tar.gz
mv nginx-1.18.0 nginx
```

3、安装 Nginx
```shell script
cd /usr/local/nginx
./configure
make
nginx -c /usr/local/nginx/conf/nginx.conf
```

4、配置环境变量
```shell script
vim /etc/profile

#文件最下方添加
export PATH=$PATH:/usr/local/nginx/sbin

#保存退出执行
source /etc/profile

#测试环境变量是否成效
nginx -v
```

5、安装nodejs

[下载 Linux 二进制文件](https://npm.taobao.org/mirrors/node/v14.15.4/)
```shell script
cd /usr/local
#上传文件
tar -xvf node-v14.15.4-linux-x64.tar.xz  
mv node-v14.15.4-linux-x64 nodejs
```

6、配置环境变量
```shell script
vim /etc/profile

#文件最下方添加
export PATH=$PATH:/usr/local/nodejs/bin

#保存退出执行
source /etc/profile

#测试环境变量是否成效
node -v
npm -v
```

[目录](https://github.com/jines-z/note)
