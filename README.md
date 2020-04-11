# pic
我的图床




#### 内网穿透工具比较
(ngrok,frp,lanproxy,goproxy,nps)
https://www.wezoz.com/


#### frp
GitHub官网：https://github.com/fatedier/frp/

##### 服务端
下载服务端文件，可以放在，`/usr/local/src/frp/`，服务端默认配置为
```
[common]
bind_port = 7000
```
##### 启动服务
命令后台运行参考：https://www.cnblogs.com/jinxiao-pu/p/9131057.html
```
# 不保存输出日志
nohup /usr/local/src/frp/frps -c /usr/local/src/frp/frps.ini >/dev/null 2>&1 &

# 设置开机自启动 `vim /etc/rc.local` 加入服务启动命令：
nohup /usr/local/src/frp/frps -c /usr/local/src/frp/frps.ini >/dev/null 2>&1 &
```


##### 客户端
使用简单，配一下就跑起来了，很方便。
客户端配置示例（frpc.ini）：
```
[common]
server_addr = 122.51.217.186
server_port = 7000

admin_addr = 127.0.0.1
admin_port = 7400
admin_user = admin
admin_pwd = admin

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 40022
```
- server_addr是服务器的ip
- server_port是默认的服务器使用端口号
- admin_*是网页管理

#### ngrok
配置的时候比较麻烦，最后配好跑起来，显示connected，但是访问不了，不知道为啥。

参考：https://www.jianshu.com/p/f5c2a55e77bd
export NGROK_DOMAIN="ngrok.leostudio.top"
```
//服务器开启服务
/usr/local/src/ngrok/bin/ngrokd -domain="ngrok.leostudio.top" -httpAddr=":801" - httpsAddr=":4431" -tunnelAddr=":4443"

// 放行防火墙： 另需注意安全组
firewall-cmd --zone=public --add-port=0-65535/tcp --permanent
firewall-cmd --zone=public --add-port=4431/tcp --permanent
firewall-cmd --reload
```

