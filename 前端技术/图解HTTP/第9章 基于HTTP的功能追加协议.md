## 第9章 基于HTTP的功能追加协议

### 9.2 消除HTTP瓶颈的SPDY

#### 9.2.2 SPDY的设计与功能

SPDY没有完全改写HTTP协议，而是在TCP/IP的应用层与传输层之间通过新加会话层的形式运作，使用SSL通信。

使用SPDY后，HTTP协议额外获得以下功能：

- 多路复用流：通过单一TCP连接，可以处理多个HTTP请求。
- 赋予请求优先级：给请求逐个分配优先级顺序。
- 压缩HTTP Header
- 推送功能
- 服务器提示功能：服务器可以主动提示客户端请求所需的资源。



### 9.3 使用浏览器进行全双工通信的 WebSocket

#### 9.3.2 WebSocket协议

主要特点：

- 推送功能：支持由服务器向客户端推送数据的推送功能。
- 减少通信量：和HTTP相比，每次连接时的总开销减少，Header信息减少。

为了实现WebSocket通信，需要用刀HTTP的Upgrade Header，告知服务器通信息以发生改变，以达到握手目的。

`Upgrade: websocket`

服务器对于该请求，返回101 Switching Protocols 的响应。

JS可调用 WebSocket API 实现WebSocket 歇一下的全双工通信，例如：

```JS
var socket = new WebSocket('ws://game.example.com:12010/updates')
socket.onopen = () => {
    setInterval(()=>{
        if(socket.bufferedAmount == 0) {
            socket.send(getUpdateData())
        }
    }, 50)
}
```

