# frontEndHandbook
整理的关于前端的一些知识，不定期更新。

#### 关于缓存
##### (1) 为什么要缓存？
- 减少带宽消耗
- 降低服务器压力（用户和爬虫角度）
- 提升用户体验
- https://www.cnblogs.com/btgyoyo/p/6125159.html
##### (2) 有哪些缓存？
- 数据库缓存
- CDN 缓存
- 代理服务器缓存
- 浏览器缓存
- 应用层缓存

##### (3) 怎么做？
##### (4) CDN 和代理服务器的区别是什么？
- CDN 加速静态资源，反向代理做动态资源的负载均衡
- 什么是CDN？如果我在广州访问杭州的淘宝网，跨省的通信必然造成延迟。如果淘宝网能在广东建立一个服务器，静态资源我可以直接从就近的广东服务器获取，必然能提高整个网站的打开速度，这就是CDN。CDN叫内容分发网络，是依靠部署在各地的边缘服务器，使用户就近获取所需内容，降低网络拥塞，提高用户访问响应速度。
- 反向代理，代理服务器，降低用户对系统的理解复杂度。
##### (5) 缓存和304 的关系 
304 表示未修改，意思就是自从上次缓存过后页面未被修改过。那么这个未修改是如何定义的，可以通过以下两种方式：Last-modified & ETag

- Last-modified 的意思就是说每次服务器有修改的时候会告诉客户端修改时间是多少，客户端下次请求的时候会携带这个数据让服务器检查从这个时间以后是否有发生过修改，如果没有则返回304，如果有修改则返回200 以及请求的内容。
- ETag 是请求内容的一个hash 值，服务器返回给客户端请求内容的同时会返回一个ETag，客户端下次请求同样的内容时会携带ETag，服务器端通过对比这个ETag 和目前做的ETag 来判断资源是否被修改。如未被修改则返回304，否则返回200.
- ETag 相对于Last-modified 的优势
![etag](./img/etag.png)
- http://web.jobbole.com/85243/
##### (6) CDN 和DNS 的关系
网页打开的时候先去找DNS 拿到最近的CDN 服务器地址，然后去请求CDN 服务器，CDN 服务器去请求真正的服务器拿数据并缓存。
##### (7) 强缓存和协商缓存
- 强缓存：直接读缓存
- 协商缓存：先确定缓存是否有效（304）
- https://www.cnblogs.com/wonyun/p/5524617.html 

---
#### 关于Http
##### (1) Http 历史
![his](./img/his.png)
##### (2) Http 基本优化
- 影响Http 网络请求速度的因素：带宽和延迟
    - 延迟包含：
        - 浏览器阻塞，对于同一个域名，请求数有限制，超过最大请求数就会阻塞
        - DNS 查询，可以利用DNS 缓存优化
        - 建立连接，三次握手
##### (3) Http 1.0 与Http 1.1
- 缓存处理：1.0 使用If-Modified-Since,Expires。1.1 引入更多的缓存策略如Entity tag，If-Unmodified-Since, If-Match, If-None-Match。
- 带宽优化及网络连接使用：1.1 允许请求资源的某个部分，返回码是206
- 错误通知处理：1.1 增加多个错误响应状态码
- Host 头处理：1.0 默认一台主机只有一个ip，但是1.1 不一样，需要写到host 头部信息
- 长连接：1.1 默认长连接，可以在一个tcp 连接上发送多个http 相应和请求
- 存在的问题
    - 多次建立连接，增大延迟
    - 明文传输，不安全
    - header 里携带的内容过大，且每次不怎么变化，浪费流量
    - 长连接使用多了会造成性能压力
##### (4) Http 与Https
- 网景于1994 年创建Https
- Https = Http + SSL(TLS)
- Http 端口80，Https 端口443
- Https 是通过对明文信息进行加密保证信息的安全性，防止运营商劫持。涉及到加密就需要有密码，为了保证安全性需要使用非对称加密 + 对称加密的方式进行。涉及到非对称加密就要有公钥和私钥，涉及到公钥私钥就要有证书，因此Https 协议需要向CA 购买证书。
##### (5) Https 与Http2
- Https 消耗大，只能解决安全问题，解决不了性能问题，而且加解密的过程实际上会造成性能问题。于是出现了Http2
- Http2 支持明文传输、使用新的二进制格式、压缩消息头、多路复用（连接共享，只有一个Tcp 连接，双工通信）、服务端推送