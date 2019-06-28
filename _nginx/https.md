### https配置

[nginx https配置](https://blog.csdn.net/smartdt/article/details/80027579)

```js
1. 默认的nginx配置没有http_ssl_modules模块，需要重新配置

通过命令查看是否配置

/usr/local/nginx/sbin/nginx -V

2. 配置http_ssl_mudules

 2.1 进入到nginx目录(下载的文件包目录，不是安装目录)
 
 ./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module
 
 2.2 编译
 
 make
 
3.nginx配置文件配置

下载nginx配置的https证书

cert目录在conf目录下

server {
    listen       443 default ssl;
    server_name  localhost;
    ssl on;
    root html;
    index index.html index.htm;
    ssl_certificate      cert/xiaoyueyue.crt;
    ssl_certificate_key  cert/xiaoyueyue.key;

    ssl_session_cache    shared:SSL:1m;
    ssl_session_timeout  5m;

    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    location / {
        root   html;
        index  index.html index.htm;
    }
}
```