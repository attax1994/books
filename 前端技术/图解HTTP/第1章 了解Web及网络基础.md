## 第1章 了解Web及网络基础

### 1.3  网络基础 TCP / IP
四层模型：
- 应用层：HTTP、FTP、DNS等应用协议。
- 传输层：TCP和UDP。
- 网络层：IP层。
- 数据链路层：MAC层。



### 1.4 与HTTP关系密切的协议：IP、TCP和DNS

#### 1.4.1 负责传输的IP协议

IP间的通信依赖MAC地址。

MAC与IP地址之间的映射采用ARP协议（Address Resolution Protocol）。

#### 1.4.2 确保可靠性的TCP协议

**三次握手**

- 第一次握手：主机A发送位码为SYN=1，随机产生序列seq number的数据包到服务器，服务器B由SYN=1知道，A需要建立连接。
- 第二次握手：服务器B收到后要求确认联机信息，向A发送ack number（主机A的seq number + 1），SYN=1，ACK=1的包，随机产生seq。
- 第三次握手：主机A收到ACK，检查number是否正确（为自己发送的seq number + 1），以及位码ACK是否为1。若正确，主机会再次发送ack number（主机B的seq number + 1），ACK=1。主机B收到后确认seq值和ACK位码，则连接建立成功。

**四次挥手**

- 客户端A发送一个FIN.用来关闭主机A与服务器B之间的数据传送(报文段4)。
- 服务器B收到这个FIN. 它发回一个ACK，确认序号为收到的序号+1(报文段5)。和SYN一样，一个FIN将占用一个序号。
- 服务器B关闭与主机A的连接，发送一个FIN给客户端A(报文段6)。
- 客户端A发回ACK报文确认，并将确认序号设置为序号加1(报文段7)。



### 1.7 URI和URL

URI（Uniform Resource Identifier）：统一资源标识符，通常是`协议:登录信息@服务器地址:端口号/文件路径?query#hash`的形式，如`http://user:pass@www.example.com:80/dir/index.html?uid=1#ch1`

URL（Uniform Resource Locator）：统一资源定位符



