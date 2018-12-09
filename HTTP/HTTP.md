<h1>一些知识点</h1>

1. 􏰨通过发送请求服务器资源的 Web 浏览器等，都可􏰩为客户端(client)。

2. Web 使用一种名为 HTTP(HyperText Transfer Protocol，超文本传输协议)的协议作为规范，完成从客户端到服务器端等一运作流程 。

3. 通常使用的网络(包括互联网)是在 TCP/IP 协议􏲳的基础上运作的。而 HTTP属于它内部的一个。

   <img src="https://github.com/zhuxinyu/blog/blob/master/HTTP/WX20181209-143449%402x.png" width = "440" height = "225" div align=center />

4. TCP/IP协议族各层的作用：

   - **应用层**: 向用户提供应用服务时通信的活动。

     FTP（File Transfer Protocol, 文本传输协议）

     DNS (Domain Name System, 域名系统)

     HTTP (HyperText Transfer Protocol, 超文本转换协议)

   - **传输层**:对上层应用层，提供处于网络链接中的两台计算机之间的数据传输。

     - TCP (Transmission Control Protocol, 传输控制协议)
     - UDP (User Data Protocol, 用户数据报协议)

   - **网络层**(又名网络互连层)：处理在网络上流动的数据包。网络层所起的作用就是在众多的选项内选择一条传输线路。

   - **链路层**(又名数据链路层，网络接口层)：处理链接网络的硬件部分，包括控制操作系统、硬件的设备驱动、NIC(Network Interface Card，网络适配器即网卡)，及光纤等物理可见部分（还包括连接器等一切传输媒介），硬件上的范畴均在链路层的作用范围内。

     <table><tr>
         
     </table>

     <table><td><img src="https://github.com/zhuxinyu/blog/blob/master/HTTP/WX20181209-145440%402x.png" width = "350" height = "230" div align=left /></td>

     <td><img src="https://github.com/zhuxinyu/blog/blob/master/HTTP/WX20181209-145849%402x.png" width = "350" height = "230" div align=left /></td>

     </tr></table>

5. 把数据信息包装起来的做法成为封装(encapsulate).

6. 与HTTP关系密切的协议:**IP**(Internet Protocol，网际协议),**TCP**,**DNS**

   - 负责传输的IP协议：(网络层)

     作用是把各种数据包传递给对方，通过网络地址（IP）和物理地址(MAC), IP间的通信通过ARP协议（Address Resolution Protocol）反查出对应的MAC地址，通过路由选择（routing）的方式转发给下一站，直到目的地。

   - 确保可靠性的TCP协议:(传输层)

     提供可靠地字节流服务，可靠性指为确保数据能到达目标采用三次握手策略(three-way handshaking)，字节流指将大块数据分割成以报文段（segment）为单位的数据包进行管理。

   - 负责域名解析的DNS服务:（应用层）

     提供域名到IP地址之间的解析服务

     **各种协议与HTTP协议的关系，如下图所示**<br>

     <img src="https://github.com/zhuxinyu/blog/blob/master/HTTP/WX20181209-152014%402x.png" width = "450" height = "700" div align=center /><br>







   <一些关键点>



   1. HTTP用于客户端和服务器端的通信

   2. 通过请求响应交换数据，一次请求一次响应

   3. 不保存状态，若要保存状态通过cookie

   4. 通过请求URI（URL）定位资源

   5. URL包含登陆信息（认证），服务器地址，服务器端口号，带层次的文件路径，查询字符串，片段标识符

   6. GET:获取资源

      POST: 传输尸体主题

      PUT:传输文件

      HEAD:获取报文首部

      DELETE:删除文件

      OPTIONS:询问支持的方法

      TRACE:追踪路径

      CONNECT:要求用隧道协议连接代理（主要使用SSL（Secure Sockets Layer，安全套接层）和TLS(Transport Layer Security,传输层安全)协议把通信内容加密后经网络隧道传输）CONNECT 代理服务器名：端口号 HTTP版本

   7. 持久性链接 HTTP keep-alive,只要任意一段没有明确提出断开连接，则保持TCP连接状态，好处在于减少了TCP连接的重复建立和断开所造成的额外开销，减轻了服务器端的负载，请求和响应速度也更快。

   8. 提高传输速率的几种方法：

      - 压缩传输的内容编码:

        gzip (GNU zip)

        compress (UNIX 系统的标准压缩)

        deflate (zlib)

        identity (不进行编码)

      - 分隔发送的分块传输编码(Chunked Transfer Coding)：传输编码(Transfer coding)机制，只定义作用于分块传输编码

   9. 多部分对象集合的数据发送：(文本，视频，图片等，采用MIME(Multipurpose Internet Mail Extensions，多用途因特网邮件扩展)机制)

      - multipart/form-data: 在web表单文件上传时使用
      - multipart/byteranges: 状态码206(partial content,部分内容)响应报文包含了多个范围的内容时使用

   10. 使用Range获取范围内部分内容：解决中继传输等问题

   11. 内容协商机制是指客户端和服务器端就相应的资源内容进行交涉，然后提供给客户端最为合适的资源。内容协商会以响应资源的语言、字符集、编码方式等作为判断的基准。

       - 服务商驱动协商(Server-driven Negotiation)：以服务器端进行内容协商
       - 客户端驱动协商(Agent-driven Negotiation): 以客户端驱动协商
       - 透明协商(Transparent Negotiation):是服务器驱动和客户端驱动的结合体，是由服务器端和客户端各自进行内容协商的一种方法。

   12. 状态码的类别：

       - 1xx: Informational(信息性状态码)：接收的请求正在处理
       - 2xx：Success（成功状态码）：请求正常处理完毕
       - 3xx：Redirection(重定向状态码)：需要进行附加操作以完成请求
       - 4xx：Client Error(客户端错误状态码)：服务器无法处理请求
       - 5xx：Server Error（服务器错误状态码）： 服务器处理请求出错

   13. 用单台虚拟主机可实现多个域名，也就是多个域名映射到同一个ip地址

   14. HTTP的缺点：（未加密协议共性缺点）

       - 通信使用明文（不加密），内容可能会被窃听
       - 不验证通信方的身份，因此有可能遭遇伪装
       - 无法证明报文的完整性，所以有可能已遭篡改

   15. 加密处理防止被窃听：

       1. 通信加密，与SSL(Secure Socket Layer)和TLS(Transport Layer Security)组合使用的HTTP被称为HTTPS(HTTP Secure,超文本传输安全协议)或HTTP over SSL.
       2. 内容加密，仍有被篡改的风险

   16. 不验证通信方的身份就可能遭遇伪装：查明对手的证书

   17. 接收到的内容可能有误：常用MD5和SHA-1等散列值校验方法，以及用来确认文件的数字签名。

   18. 请求或相应在传输途中，遭攻击者拦截并篡改内容的攻击成为中间人攻击(Man-in-the-Middle attack,MITM)

   19. HTTP + 加密 + 认证 + 完整性保护 = HTTPS

   20. SSL是独立于HTTP的协议，所以不光是HTTP协议，其他运行在应用层的SMTP和Telnet等协议均可配合SSL协议使用。可以说SSL是当今世界上应用最为广泛的网络安全技术。

   21. HTTP的瓶颈：

       - 一条连接上只可发送一个请求
       - 请求只能从客户端开始。客户端不可以接收除响应以外的指令
       - 请求/响应首部未经压缩就发送。首部信息越多延迟越大
       - 发送冗长的首部。每次互相发送相同的首部造成的浪费较多。
       - 可任意选择数据压缩格式。非强制压缩发送

   22. SPDY 消除HTTP瓶颈：（会话层，采用HTTP建立通信连接，通信中使用SSL）

       - 多路复用流：通过单一的TCP链接，可以无限制处理多个HTTP请求。所有请求的处理都在 一条TCP连接上完成，因此TCP的处理效率得到提高
       - 赋予请求优先级：主要为了在发送多个请求时，解决因带宽低而导致响应变慢的问题
       - 压缩HTTP请求和响应的首部：通信产生的数据包数量和发送的字节数就更少了
       - 推送功能：服务器可直接发送数据，而不必等待客户端的请求
       - 服务器提示功能：服务器可以主动提示客户端请求所需的资源。由于在客户端发现资源之前就可以获知资源的存在，因此在资源已缓存的情况下，可以避免发送不必要的请求。

   23. SPDY的实用性问题：

       - 只是将当个域名的通信多路复用，所以当一个Web网站上使用多个域名下的资源，改善效果就会受到限制
       - 很多Web网站存在的问题并非仅仅是由HTTP瓶颈所导致。对Web本身速度的提升，还应该从其他可细致钻研的地方入手

   24. 使用全双工通信WebSocket消除HTTP瓶颈：一但确立WebSocket通信连接，不论服务器还是客户端，任意一方都可直接向对方发送报文（建立于HTTP基础上的协议）

       - 推送功能：服务器可直接发送数据，不必等待客户端的请求
       - 减少通信量： 只要建立起WebSocket链接，就希望一直保持连接状态。不仅连接时总开销减少，由于首部信息很小，通信量也响应减少
       - 为了实现WebSocket通信，在HTTP连接建立后，需要弯沉过一次握手的步骤

   25. HTTP/2.0:

       - SPDY
       - HTTP Speed + Mobility (微软， 改善并提高移动端通信时的通信速度和性能的标准，建立于Google提出的SPDY与WebSocket的基础之上)
       - Network-Friendly HTTP Upgrade （在移动端通信时改善HTTP性能）

   26. HTML5标准不仅解决了浏览器之间的兼容性问题，并且可把文本作为数据对待，更容易复用，动画等效果也变得更生动。

   27. CSS(Cascading Style Sheets,层叠样式表)可以指定如何展现HTML内的各种元素，属于样式表标准之一。CSS理念就是让文档的结构和设计分离，达到解耦的效果。

   28. 动态HTML技术是通过调用客户端脚本语言JavaScript，实现对HTML的Web页面的动态改造。利用DOM(Document Object Model， 文档对象模型)可指定欲发生动态变化的HTML元素。

   29. CGI(Common Gateway interface,通用网关接口是指Web服务器在接收到客户端发送过来的请求后转发给程序的一组机制)。CGI程序通常使用Perl、PHP、Ruby和C等语言编写

   30. XML（eXtensible Markup Language, 可扩展标记语言）是一种可按应用目标进行扩展的通用标记语言。旨在使互联网数据共享变得更容易。

   31. JSON（JavaScript Object Notation）是一种以JavaScript（ECMAScript）的对象表示法为基础的轻量级数据标记语言。能够处理的数据类型有false/null/true/对象/数组/数字/字符串，这7种类型。
