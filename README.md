## frp

1. 通过应用服务器的公网 IP 做内网穿透
2. frps 与 frpc 是通过配置的 7000 做通信的

## feature

1. frp client

   - 热加载 frpc.ini

     ```conf
     frpc reload -c ./frpc.ini
     ```

   - 默认配置了 7400 作为 frpc 的管页面
   - 批量端口暴露

     ```conf
     [range:tcp_port]
     type = tcp
     local_ip = 127.0.0.1
     local_port = 6010-6020,6022,6024-6028
     remote_port = 6010-6020,6022,6024-6028
     use_encryption = false
     use_compression = false
     ```

2. frp server

   - 默认配置了 7500 作为 frps 的管理页面

## issue

1. propagations

   - 多个 frp 客户端间的连接

2. 相关参数安全问题

   - [docker var] - [build] - [env](https://github.com/fatedier/frp#using-environment-variables)

---

## reference

1. https://gitee.com/spoto/natserver
2. https://github.com/snowdreamtech/frp
3. https://github.com/fatedier/frp
4. https://github.com/fatedier/frp/blob/dev/conf/frpc_full.ini
5. https://github.com/fatedier/frp/blob/dev/conf/frps_full.ini
