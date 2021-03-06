## 第7章 确保Web安全的HTTPS

### 7.1 HTTP的缺点

- 通信使用明文（不加密），内容可能会被窃听
  - 通信加密：使用SSL或TLS加密HTTP通信内容
  - 内容加密：对HTTP协议传输的内容本身加密
- 不验证通信方的身份，因此有可能遭遇伪装
  - 查明对手的证书：SSL不仅提供加密处理，而且还使用了第三方颁发的证书
- 无法证明报文的完整性，所以有可能已遭篡改
  - 防止内容篡改：使用MD5或SHA-1等散列值校验方法，以及验证数字签名



### 7.2 HTTP + 加密 + 认证 + 完整性保护 = HTTPS

- HTTP加上加密处理和认证以及完整性保护后即是HTTPS
- HTTPS是身披SSL外壳的HTTP
- 相互交换密钥的公开密钥技术
- 证明公开密钥正确性的证书

HTTPS的通信步骤：

1. 客户端通过发送 Client Hello 报文开始SSL通信。报文中包含客户端支持的SSL指定版本、加密组件列表（算法及密钥长度）。
2. 服务器可进行SSL通信时，会以 Server Hello 报文作为应答。报文中包含SSL版本和加密组件。
3. 服务器发送 Certificate 报文。报文中包含公开密钥证书。
4. 服务器发送 Server Hello Done 报文通知客户端，最初阶段的SSL握手协商部分结束。
5. SSL第一次握手结束后，客户端以 Client Key Exchange 报文作为回应。报文中包含通信加密中使用的 Pre-master secret 随机密码串，并使用公钥加密。
6. 客户端继续发送 Change Cipher Spec 报文。该报文会提示服务器，在此报文之后的通信会采用 Pre-master secret 密钥加密。
7. 客户端发送 Finished 报文。包含连接至今全部报文的整体校验值。
8. 服务器同样发送  Change Cipher Spec 报文。
9. 服务器同样发送 Finished 报文。
10. SSL连接建立完成，开始进行应用层协议的通信，发送HTTP请求。
11. 应用层协议通信，发送HTTP响应。
12. 通信结束后，客户端断开连接，发送 close_notify 报文。

