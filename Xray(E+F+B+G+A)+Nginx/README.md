介绍：

利用 Nginx 支持 SNI 分流特性，对 VLESS+Vision+TLS、Trojan+TCP+TLS、HTTPS server 进行 SNI 分流（四层转发），实现除 Xray 的 mKCP 应用外共用 443 端口。其中 Nginx 同时为 VLESS+Vision+TLS 与 Trojan+TCP+TLS 提供回落服务（WEB 服务），为 Xray 的 WebSocket、gRPC 提供反向代理，其应用如下：

1、E=VLESS+Vision+TLS（回落/分流配置，TLS由自己启用及处理。）

2、F=Trojan+TCP+TLS（回落/分流配置，TLS由自己启用及处理。）

3、B=VMess+WebSocket+TLS（TLS由Nginx启用及处理，不需配置。）

4、G=Shadowsocks+gRPC+TLS（TLS由Nginx启用及处理，不需配置。）

5、A=VLESS+mKCP+seed

注意：

1、Nginx 支持 SNI 分流需要 Nginx 包含 stream_core_module 和 stream_ssl_preread_module 模块。

2、Xray 的监听地址不支持 Shadowsocks（简称SS） 协议使用 UDS 监听。

3、Xray 版本不小于 v1.7.2 才完美支持 VLESS 协议的 XTLS Vision 应用。

4、Nginx 支持 H2C server、HTTP/2 server 及 gRPC proxy 需要 Nginx 包含 http_ssl_module 与 http_v2_module 模块及 OpenSSL 库。

5、Nginx 支持 H2C server，但不支持 HTTP/1.1 server 与 H2C server 共用一个端口或一个进程；故回落分成 http/1.1 回落与 h2 回落分别对应 Nginx 的 HTTP/1.1 server 与 H2C server。

6、Nginx 支持请求标头还原为真实客户端地址需要 Nginx 包含 http_realip_module 模块。

7、不要使用 ACME 客户端在采用本示例的服务器上以 HTTP-01 或 TLS-ALPN-01 验证方式申请与更新 TLS 证书，因 HTTP-01 或 TLS-ALPN-01 验证方式申请与更新 TLS 证书需监听 80 或 443 端口，从而与当前应用端口冲突。

8、配置1：使用 Local Loopback 连接，且启用了 PROXY protocol。配置2：使用 UDS 连接（对应 Shadowsocks+gRPC+TLS 除外），且启用了 PROXY protocol。

9、本示例 F 兼容原版 Trojan 应用，即可使用 Trojan 客户端 或 Trojan-Go 客户端对应连接。
