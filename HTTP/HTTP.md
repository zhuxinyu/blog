<h1>第一章 了解Web及网络基础</h1>

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

     <td><img src="https://github.com/zhuxinyu/blog/blob/master/HTTP/WX20181209-145440%402x.png" width = "350" height = "230" div align=left /></td>

     <td><img src="https://github.com/zhuxinyu/blog/blob/master/HTTP/WX20181209-145849%402x.png" width = "350" height = "230" div align=right /></td>

     </tr></table>

   <br>

5. 把数据信息包装起来的做法成为封装(encapsulate).

6. 与HTTP关系密切的协议:**IP**(Internet Protocol，网际协议),**TCP**,**DNS**

   - 负责传输的IP协议：(网络层)

     作用是把各种数据包传递给对方，通过网络地址（IP）和物理地址(MAC), IP间的通信通过ARP协议（Address Resolution Protocol）反查出对应的MAC地址，通过路由选择（routing）的方式转发给下一站，直到目的地。

     <img src="https://github.com/zhuxinyu/blog/blob/master/HTTP/WX20181209-151115%402x.png" width = "350" height = "230" div align=left />

