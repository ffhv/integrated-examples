介绍：

利用 Nginx 支持 WebSocket、gRPC 代理，实现除 Xray 或 V2Ray 的 mKCP 应用外，WebSocket、gRPC 两种类型的反向代理应用共用 443 端口，其应用如下：

1、B=VMess+WebSocket+TLS（TLS由Nginx启用及处理，不需配置。）

2、G=Shadowsocks+gRPC+TLS（TLS由Nginx启用及处理，不需配置。）

3、A=VLESS+mKCP+seed

注意：

1、Nginx 支持不同站点共用 443 端口需要 Nginx 包含 stream_core_module 和 stream_ssl_preread_module 模块。

2、Nginx 支持 HTTPS server、HTTP/2 server 及 WebSocket proxy、gRPC proxy 需要 Nginx 包含 http_ssl_module 与 http_v2_module 模块及 OpenSSL 库。

3、Nginx 支持请求标头还原为真实客户端地址需要 Nginx 包含 http_realip_module 模块。

4、Xray 或 V2Ray 的监听地址不支持 Shadowsocks（简称SS） 协议使用 UDS 监听。

5、Xray 版本不小于 v1.4.0 或 V2Ray 版本不小于 v4.36.2 才支持 gRPC 传输方式。

6、不要使用 ACME 客户端在采用本示例的服务器上以 HTTP-01 或 TLS-ALPN-01 验证方式申请与更新 TLS 证书，因 HTTP-01 或 TLS-ALPN-01 验证方式申请与更新 TLS 证书需监听 80 或 443 端口，从而与当前应用端口冲突。

7、配置1：使用 Local Loopback 连接。配置2：使用 UDS 连接（对应 Shadowsocks+gRPC+TLS 除外）。
