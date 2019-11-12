# Vue 部署到nginx服务器（Windows系统）
```
目的：1.解决前后端分离网站和后台服务跨域问题
      2.可以配置多个上游服务器，解决负载均衡问题
```

## 1.Vue-cli项目在开发时如何配置反向代理
```
下面的代理仅仅开发时有效
  devServer: {
    port: 8080,
    proxy: {
      '/mapBaseUrl': {
        target: 'http://192.168.0.2*:8080',
        ws: true,
        changeOrigin: true,
        pathRewrite: {
          '^/mapBaseUrl': ''
        }
      },
      '/threeDTiles': {
        target: 'http://117.159.25.*2:18980',
        ws: true,
        changeOrigin: true,
        pathRewrite: {
          '^/threeDTiles': ''
        }
      }
    }
  },
``` 



## 2.Vue-cli项目在部署后如何在nginx配置反向代理
```
下载nginx windows 安装包

编辑nginx.conf 配置文件如下
```
### 2.1.Vue-cli项目在部署后如何在nginx配置反向代理
```  
nginx.conf配置如下 
    server {
        listen       10086;
        server_name  localhost;  

        location  / {
            root   F:\Code\luolong\dist; //指向dist文件夹
            index  index.html index.htm;
        }

        location /mapBaseUrl {
             rewrite  ^.+mapBaseUrl/?(.*)$ /$1 break;
             include  uwsgi_params; 
             proxy_pass http://117.159.25.*2:18983;  
        }

        location /threeDTiles {
             rewrite  ^.+threeDTiles/?(.*)$ /$1 break;
             include  uwsgi_params; 
             proxy_pass http://117.159.25.*2:18980;  
        }   
    }
```

### 2.2.启动网站
```
cmd  start nginx
http://localhost:10086/
```
 
