**这里是分享怎么搭建主流科学上网的优化配置及最优组合示例（如是不太了解科学上网，建议先依次从简单到复杂参考及部署。），其特点如下：**  
1. 实现了反代使用Local Loopback连接或使用Unix Donew Socket（UDS）连接支持。
2. 实现了回落/分流使用Local Loopback连接或使用Unix Donew Socket（UDS）连接及启用PROXY protocol支持。
3. 实现了SNI分流使用Local Loopback连接或使用Unix Donew Socket（UDS）连接及启用PROXY protocol支持。
4. 实现了Caddy、Xray/V2Ray使用UDS连接时采用Abstract sockets模式（不需考虑权限问题）。
5. 实现了Nginx SNI分流（TCP转发）与定向UDP转发配合以支持SNI分流后的NaiveProxy HTTP/3代理应用。
6. 实现了使用json配置Caddy SNI分流，灵活性等同HAProxy SNI分流。
7. 实现了Caddy与相关应用的TLS证书申请与更新全自动化。
8. 实现了服务端综合应用配置示例中使用mKCP、WebSocket、HTTP/2、gRPC传输方式的应用配置可删、可换、可增（套娃实现REALITY H2/gRPC应用除外），灵活组合而不影响整体架构。
9. 实现了除Xray/V2Ray mKCP与Hysteria应用之外，其它应用对外都使用443端口，各应用互不影响。
10. 实现了正常应用与CDN流量中转（基于WebSocket over TLS或基于gRPC over TLS）同时使用。
11. 实现了除Xray/V2Ray的mKCP应用与Hysteria应用之外，其它应用都支持流量伪装与防探测，且提供流量伪装与防探测的回落或代理网站都支持HTTP自动跳转到HTTPS，SSL/TLS安全评估报告为A+（非AES算法的密码套件配置示例除外）等，即所有特征完全与真实网站一致。

### 服务端单一/简单应用配置示例
#### &emsp;Xray/V2Ray的mKCP应用与Hysteria应用
1. [V2Ray(VLESS\VMess+mKCP+seed)](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(VLESS%5CVMess%2BmKCP%2Bseed))（VLESS/VMess+mKCP+seed应用。VLESS+mKCP+seed标记为A。）
2. [Hysteria](https://github.com/lxhao61/integrated-examples/tree/new/Hysteria)（基于QUIC协议修改的双边加速代理应用。）
#### &emsp;反代Xray/V2Ray的WebSocket应用
1. [V2Ray(VMess+WebSocket)+Caddy\Nginx](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(VMess%2BWebSocket)%2BCaddy%5CNginx)（VMess+WebSocket+TLS应用。标记为B。）
2. [V2Ray(SS+Door+WebSocket)+Caddy](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(SS%2BDoor%2BWebSocket)%2BCaddy%5CNginx)（兼容Shadowsocks加v2ray-plugin插件的websocket-tls应用。）
3. [V2Ray(VLESS+WebSocket)+Caddy\Nginx](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(VLESS%2BWebSocket)%2BCaddy%5CNginx)（VLESS+WebSocket+TLS应用。）
4. [V2Ray(Trojan+WebSocket)+Caddy\Nginx](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(Trojan%2BWebSocket)%2BCaddy%5CNginx)（Trojan+WebSocket+TLS应用。标记为C。）
#### &emsp;反代Xray/V2Ray的H2C应用
1. [V2Ray(VLESS+H2C)+Caddy](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(VLESS%2BH2C)%2BCaddy)（VLESS+H2C+TLS应用。标记为D。）
2. [V2Ray(Trojan+H2C)+Caddy](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(Trojan%2BH2C)%2BCaddy)（Trojan+H2C+TLS应用。）
#### &emsp;反代Xray/V2Ray的gRPC应用
1. [V2Ray(VMess+gRPC)+Caddy\Nginx](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(VMess%2BgRPC)%2BCaddy%5CNginx)（VMess+gRPC+TLS应用。）
2. [V2Ray(SS+gRPC)+Caddy\Nginx](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(SS%2BgRPC)%2BCaddy%5CNginx)（兼容Shadowsocks加v2ray-plugin插件的grpc-tls应用。标记为G。）
3. [V2Ray(VLESS+gRPC)+Caddy\Nginx](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(VLESS%2BgRPC)%2BCaddy%5CNginx)（VLESS+gRPC+TLS应用。）
4. [V2Ray(Trojan+gRPC)+Caddy\Nginx](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(Trojan%2BgRPC)%2BCaddy%5CNginx)（Trojan+gRPC+TLS应用。）
#### &emsp;Xray的VLESS与Trojan回落应用
1. [Xray(VLESS+Vision+TLS)+Nginx](https://github.com/lxhao61/integrated-examples/tree/new/Xray(VLESS%2BVision%2BTLS)%2BNginx)（VLESS+Vision+TLS回落Nginx。标记为E。）
2. [Xray(VLESS+Vision+TLS)+Caddy](https://github.com/lxhao61/integrated-examples/tree/new/Xray(VLESS%2BVision%2BTLS)%2BCaddy)（VLESS+Vision+TLS回落Caddy。标记为E。）
3. [Xray(Trojan+TCP+TLS)+Nginx](https://github.com/lxhao61/integrated-examples/tree/new/Xray(Trojan%2BTCP%2BTLS)%2BNginx)（Trojan+TCP+TLS回落Nginx应用。标记为F。）
4. [Xray(Trojan+TCP+TLS)+Caddy](https://github.com/lxhao61/integrated-examples/tree/new/Xray(Trojan%2BTCP%2BTLS)%2BCaddy)（Trojan+TCP+TLS回落Caddy应用。标记为F。）
#### &emsp;Caddy插件应用
1. [NaiveProxy(Caddy+forwardproxy)](https://github.com/lxhao61/integrated-examples/tree/new/NaiveProxy(Caddy%2Bforwardproxy))（基于Caddy插件的NaiveProxy应用。标记为N。）
2. [Trojan-Go(Caddy+caddy-trojan)](https://github.com/lxhao61/integrated-examples/tree/new/Trojan-Go(Caddy%2Bcaddy-trojan))（基于Caddy插件的Trojan-Go应用。标记为T。）
3. [Caddy(N+T)](https://github.com/lxhao61/integrated-examples/tree/new/Caddy(N%2BT))（基于Caddy插件的NaiveProxy与Trojan-Go应用。）
#### &emsp;Xray的REALITY H2应用
1. [Xray(VLESS+H2C+REALITY)](https://github.com/lxhao61/integrated-examples/tree/new/Xray(VLESS%2BH2C%2BREALITY))（VLESS+H2C+REALITY应用。标记为K。）
#### &emsp;Xray的REALITY gRPC应用
1. [Xray(SS+gRPC+REALITY)](https://github.com/lxhao61/integrated-examples/tree/new/Xray(SS%2BgRPC%2BREALITY))（Shadowsocks+gRPC+REALITY应用。标记为L。）
#### &emsp;Xray的REALITY Vision应用
1. [Xray(VLESS+Vision+REALITY)](https://github.com/lxhao61/integrated-examples/tree/new/Xray(VLESS%2BVision%2BREALITY))（VLESS+Vision+REALITY应用。标记为M。）
#### &emsp;Xray的REALITY简单应用
1. [Xray(M+K)](https://github.com/lxhao61/integrated-examples/tree/new/Xray(M+K))（VLESS+Vision+REALITY与VLESS+H2C+REALITY共用端口应用。）

### 服务端综合应用配置示例
#### &emsp;以反代为核心的综合应用
1. [V2Ray(B+G+A)+Nginx](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(B%2BG%2BA)%2BNginx)（反代WebSocket、gRPC的综合应用。）
2. [V2Ray(B+D+G+A)+Caddy(N+T)](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(B%2BD%2BG%2BA)%2BCaddy(N%2BT))（反代WebSocket、H2C、gRPC加NaiveProxy与Trojian-Go的综合应用。）
#### &emsp;以Trojan分流与回落为核心的综合应用
1. [Xray(F+C+G+A)+Nginx](https://github.com/lxhao61/integrated-examples/tree/new/Xray(F%2BC%2BG%2BA)%2BNginx)（以Trojan分流与回落Nginx为核心的综合应用。）
2. [Xray(F+C+D+G+A)+Caddy(N)](https://github.com/lxhao61/integrated-examples/tree/new/Xray(F%2BC%2BD%2BG%2BA)%2BCaddy(N))（以Trojan分流与回落Caddy为核心的综合应用。）
#### &emsp;以XTLS Vision为核心的综合应用
1. [Xray(E+B+G+A)+Nginx](https://github.com/lxhao61/integrated-examples/tree/new/Xray(E%2BB%2BG%2BA)%2BNginx)（以VLESS回落Nginx为核心的综合应用。）
2. [Xray(E+B+D+G+A)+Caddy(N+T)](https://github.com/lxhao61/integrated-examples/tree/new/Xray(E%2BB%2BD%2BG%2BA)%2BCaddy(N%2BT))（以VLESS回落Caddy为核心的综合应用。）
#### &emsp;以REALITY Vision为核心的综合应用
1. [Xray(M+K+B+G+A)+Nginx](https://github.com/lxhao61/integrated-examples/tree/new/Xray(M%2BK%2BB%2BG%2BA)%2BNginx)（由Nginx提供网站实现以REALITY Vision为核心的综合应用。）
2. [Xray(M+K+B+G+A)+Caddy(N)](https://github.com/lxhao61/integrated-examples/tree/new/Xray(M%2BK%2BB%2BG%2BA)%2BCaddy(N))（由Caddy提供网站实现以REALITY Vision为核心的综合应用。）
#### &emsp;由Nginx/Caddy兼顾SNI分流实现XTLS Vision与Trojan回落/分流为核心的综合应用
1. [Xray(E+B+F+C+G+A)+Nginx](https://github.com/lxhao61/integrated-examples/tree/new/Xray(E%2BB%2BF%2BC%2BG%2BA)%2BNginx)（由Nginx兼顾SNI分流实现的综合应用。）
2. [Xray(E+B+F+C+D+G+A)+Caddy(N)](https://github.com/lxhao61/integrated-examples/tree/new/Xray(E%2BB%2BF%2BC%2BD%2BG%2BA)%2BCaddy(N))（由Caddy兼顾SNI分流实现的综合应用。）
#### &emsp;由Nginx/Caddy兼顾SNI分流实现REALITY Vision与Trojan回落/分流为核心的综合应用
1. [Xray(M+K+F+C+B+G+A)+Nginx](https://github.com/lxhao61/integrated-examples/tree/new/Xray(M%2BK%2BF%2BC%2BB%2BG%2BA)%2BNginx)（由Nginx兼顾SNI分流实现的综合应用。）
2. [Xray(M+K+F+C+B+G+A)+Caddy(N)](https://github.com/lxhao61/integrated-examples/tree/new/Xray(M%2BK%2BF%2BC%2BB%2BG%2BA)%2BCaddy(N))（由Caddy兼顾SNI分流实现的综合应用。）
#### &emsp;由Nginx/HAProxy专职SNI分流实现兼顾各方优势的综合应用
1. [Xray(E+B+F+C+D+G+A)+Caddy(N)+Nginx\HAProxy](https://github.com/lxhao61/integrated-examples/tree/new/Xray(E%2BB%2BF%2BC%2BD%2BG%2BA)%2BCaddy(N)%2BNginx%5CHAProxy)（以Vision为核心的综合应用。）
2. [Xray(M+K+F+C+B+G+A)+Caddy(N)+Nginx\HAProxy](https://github.com/lxhao61/integrated-examples/tree/new/Xray(M%2BK%2BF%2BC%2BB%2BG%2BA)%2BCaddy(N)%2BNginx%5CHAProxy)（以REALITY Vision为核心的综合应用。）
#### &emsp;注意（以上所有示例）:
1. Xray是V2Ray的超集，更好的整体性能和独有的XTLS Vision、REALITY等一系列应用增强，且完全兼容V2Ray的v4版。
2. Xray/V2Ray单一核心应用简记：A=VLESS+mKCP+seed、B=VMess+WebSocket+TLS、C=Trojan+WebSocket+TLS、D=VLESS+H2C+TLS、E=VLESS+Vision+TLS、F=Trojan+TCP+TLS、G=Shadowsocks+gRPC+TLS、K=VLESS+H2C+REALITY、L=Shadowsocks+gRPC+REALITY、M=VLESS+Vision+REALITY。
3. Xray/V2Ray示例中各应用都配置了禁用BT。如不需要，参考‘V2Ray(Other Configuration)’中BT_config.json示例删除相关配置。
4. Caddy插件单一应用简记：N=NaiveProxy(Caddy+forwardproxy)、T=Trojan-Go(Caddy+caddy-trojan)。
5. 受限应用条件及场景，NaiveProxy的QUIC应用（即Caddy的HTTP/3代理应用）不是所有相关NaiveProxy示例都支持。
6. 目前Caddy从Let's Encrypt或ZeroSSL自动申请的TLS证书默认都为ECC证书。
7. 针对V2Ray特性，当前优先推荐使用非AES算法密码套件配置示例（仅反代示例支持），最后常规配置示例。
8. 针对Xray特性，当前优先推荐使用REALITY Vision配置示例或Vision配置示例、非AES算法的密码套件配置示例、REALITY配置示例，最后常规配置示例。
9. 当前不推荐使用WebSocket传输方式的应用直接科学上网，套CDN使用无碍。若CDN流量中转（基于WebSocket over TLS或基于gRPC over TLS）使用不可信的CDN进行中转，Xray/V2Ray示例推荐使用自身带加密的VMess或Shadowsocks协议配置；否则推荐使用自身不带加密的VLESS或Trojan协议配置。
10. 综合应用配置示例中使用mKCP、WebSocket、HTTP/2、gRPC传输方式的应用配置可删、可换、可增（套娃实现REALITY H2/gRPC应用除外）；参考‘服务端单一/简单应用配置示例’中对应配置示例修改。
11. 流量伪装与防探测网站可由其它WEB应用软件实现，其支持反代（WebSocket、gRPC及H2C）与支持回落（H2C server及HTTP/1.1 server）取决于自身，自行参考Caddy或Nginx对应配置示例。
12. 附加相关插件的Caddy程序文件已编译好，去本人Releases中下载即可。
13. Trojan-Go安卓手机客户端可以去本人Releases中下载（最末）。

### 服务端特殊应用配置示例
1. [V2Ray(Other Configuration)](https://github.com/lxhao61/integrated-examples/tree/new/V2Ray(Other%20Configuration)) （Xray或V2Ray的特色应用配置方法。）
2. [Caddy(Other Configuration)](https://github.com/lxhao61/integrated-examples/tree/new/Caddy(Other%20Configuration)) （Caddy的特色应用配置方法。）

### 原版客户端配置示例
&emsp;[Client Configuration](https://github.com/lxhao61/integrated-examples/tree/new/Client%20Configuration)（若使用第三方客户端参考即可。）

### systemd服务文件
&emsp;[Service Configuration](https://github.com/lxhao61/integrated-examples/tree/new/Service%20Configuration)（配置软件服务由systemd管理。）

### 使用/贡献指南
1. 若科学上网相关软件增加新功能，开始在服务端单一应用配置示例中添加；过一段时间（测试及验证稳定后）才会服务端综合应用配置示例中添加。
2. 欢迎你提交 PR，如对现行配置示例优化修订，或将自己使用的配置制作模板提交等。
