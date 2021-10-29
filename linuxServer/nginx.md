# 禁止指定目录执行php

```bash
#单个目录
location ~* ^/uploads/.*\.(php|php5)$
{
 deny all;
}
#如果是多个目录：
location ~* ^/(attachments|uploads)/.*\.(php|php5)$
{
 deny all;
}
# 注意:以上配置文件一定要放在下面配置的前面才可以生效。
location ~ \.php$ {
fastcgi_pass  127.0.0.1:9000;
fastcgi_index index.php;
fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
include    fastcgi_params;
}
```

# vue通过NGINX部署在子目录或二级目录

1. router/index.js 添加一行
    ~~~ bash
    base : 'directory name' //配置子目录名
    ~~~

2. 根目录vite.config.ts 添加

    ~~~bash
    base: 'directory name',
    ~~~
    
3. nginx反代理部署

    ~~~nginx
    server {
       #端口随意设置
      listen 8001;
      location / {
        #必须设置，否则数由无法刷新
        try_files $uri $uri/ /index.html;
        #项目目录
        root /directory name;
        index index.html;
      }
    }
    upstream admin {
      server 127.0.0.1:3001;
    }
    
    server {
      listen 80;
      listen [::]:80;
      server_name domain name;
      access_log off;
      index index.html index.htm;
      #服务代理方式一
      location ^~/admin/ {
            proxy_redirect off;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_pass http://127.0.0.1:8001/;
      }
      #服务代理方式二
      location  /admin-api/ {
            proxy_set_header  X-Real-IP $remote_addr;
            proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header  Host $http_host;
            proxy_set_header  X-Nginx-Proxy true;
            proxy_set_header  Connection "";
            proxy_pass http://admin/;
        }
      #目录代理方式三
        location / {
            #必须设置，否则数由无法刷新
            try_files $uri $uri/ /index.html;
            #项目目录
            root /directory name;
            index index.html;
        }
    
      location ~ /admin-api/*\.(gif|jpg|jpeg|png|bmp|swf|flv|mp4|ico)$ {
        proxy_pass http://adminapi;
        expires 30d;
        access_log off;
      }
      location ~ /admin-api/*\.(js|css)?$ {
        proxy_pass http://adminapi;
        expires 7d;
        access_log off;
      }
      location ~ /(\.user\.ini|\.ht|\.git|\.svn|\.project|LICENSE|README\.md) {
        deny all;
      }
    }
    ~~~