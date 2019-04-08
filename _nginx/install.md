#### nginx 安装
1. nginx是c语言开发 编译依赖gcc环境
```
yum install gcc-c++
```
2. pcre pcre-devel安装是一个兼容正则表达式的库 
```
 yum install pcre pcre-devel
```
3. zlib 提供多种压缩和解压的方式 nginx使用zlib对http包的内容进行gzip
```
yum install zlib zlib-devel
```
4. openssl  是一个强大的安全套接字层密码库
```
yum install openssl openssl-devel
```
5. 下载nginx .tar.gz安装包
    
 + 5.1 使用wget 命令
     wget -c https://nginx.org/download/nginx-1.10.1.tar.gz
 + 5.2 解压
   tar -zvxf nginx.tar.gz
   cd nginx_1
 + 5.3 配置 查询安装模块：
 ```
 /usr/local/nginx/sbin/nginx -V
 ./configure --with-http_ssl_module 带上https服务
 ```
> 如果实现没有安装https模块，可以在继续配置[https](https://www.cnblogs.com/zhangxiaoliu/p/6183520.html)
 + 5.4 编译
 ```
   make
 ```
 + 5.5 安装
 ```
  make install
```
6. 查看安装路径
```
whereis nginx
```
7. 启动
```
cd /usr/local/nginx/sbin/
./nginx
启动nginx ： ./nginx
停用 ： ./nginx -s stop  强制杀掉进程
退出： ./nginx -s quit  待nginx进程处理任务完毕进行停止
查询： ps aux | grep nginx
重启： 先停止  ./nginx -s quit  再启动 ./nginx
重新加载配置文件： ./nginx -s reload
 ```