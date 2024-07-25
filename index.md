
curl -L https://www.cpolar.com/static/downloads/install-release-cpolar.sh | sudo bash

```
frp
[common]
# frp监听的端口，默认是7000，可以改成其他的
bind_port = 7000
#bindPort = 7000
dashboard_port = 7500
# frp管理后台用户名和密码，请改成自己的
dashboard_user = admin
dashboard_pwd = 1234
enable_prometheus = true

# 客户端配置
[common]
#服务器ip    
server_addr = 119.91.116.174
server_port = 7000
 # 与frps.ini的token一致
#token = 12345678

[socks5]
type=tcp
plugin=socks5
plugin_user=
plugin_passwd=
 #映射到共外网服务器的端口
remote_port = 8000
```
