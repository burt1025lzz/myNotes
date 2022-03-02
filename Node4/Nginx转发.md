# nginx 转发 端口

```nginx
server {
  listen       8090;  # 本机暴露外部端口
  # 		add_header 'Access-Control-Allow-Origin' 'http://192.168.1.34:7778:8090';
  # 		add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
  # 		add_header 'Access-Control-Allow-Headers' 'DNT,X-Mx-ReqToken,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Authorization';
  server_name  127.0.0.1;

  #charset koi8-r;

  #access_log  logs/host.access.log  main;
  gzip on;
  gzip_buffers 32 4K;
  gzip_comp_level 6;
  gzip_min_length 100;
  gzip_types application/javascript text/css text/xml;
  gzip_disable "MSIE [1-6]\."; #配置禁用gzip条件，支持正则。此处表示ie6及以下不启用gzip（因为ie低版本不支持）
  gzip_vary on;
  client_max_body_size 100M;
  location / {
    proxy_connect_timeout   300;
    proxy_send_timeout      300;
    proxy_read_timeout      300;
    proxy_set_header  X-Real-IP  $remote_addr;
    proxy_set_header  Client-IP  $remote_addr;
    proxy_set_header        Host $http_host;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    client_max_body_size  500m;
    proxy_pass http://192.168.1.172:8080/; # 需转发的端口
    proxy_redirect          default;
  }
}
```

------

# nginx 转发 ssh

```nginx
events {
  worker_connections  1024;
  accept_mutex on;
}
# stream 与 http 同级
stream { 
  upstream ssh {
    server IP:22;   #这里IP是虚拟机的，对应虚拟机的IP+Port
  }
  server { 
    listen 9028;  #外层通信需要的tcp端口
    proxy_pass ssh;
    proxy_connect_timeout 1h;
    proxy_timeout 1h;
  }
}
```

