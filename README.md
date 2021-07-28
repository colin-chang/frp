# frp

> frp 保姆视频教程
https://youtu.be/SlYwko8g-H8


docker images for frp(frps/frpc)

## frps

```ini
[common]
bind_port = 7000    # 客户端通信端口
vhost_http_port = 80    # HTTP端口
vhost_https_port = 443  # HTTPS端口 
token = 123456   #自定义秘钥

# dashboard
dashboard_port = 7001
dashboard_user = admin
dashboard_pwd = 123456
```

用户可以根据需要修改和挂载配置文件`frps.ini`，配置说明如上， `dashboard` 为可选。

```bash
docker pull colinchang/frps
docker run -d --name frps -p 7000:7000 -p 80:80 -p 7001:7001 -v $PWD/frps.ini:/frps/frps.ini colinchang/frps
```

## frpc
```ini
[common]
server_addr = 127.0.0.1 #frps地址或域名
server_port = 7000  #frps监听端口
token = 123456  # frps配置的密钥

# admin ui
admin_addr = 127.0.0.1
admin_port = 7400
admin_user = admin
admin_pwd = 123456

# http 示例
[web]
type = http
local_ip = 127.0.0.1
local_port = 80
remote_port = 80
custom_domains = your-domain.com # 自定义域名

# tcp 示例
[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 3306
remote_port = 3306
```
启动容器前用户务必按照实际配置修改`frpc.ini`，配置说明如上，`adminui`为可选。

```bash
docker pull colinchang/frpc
docker run -d --name frpc --network host -v $PWD/frpc.ini:/frpc/frpc.ini colinchang/frpc
```
**docker host网络模式不支持 mac OS**
