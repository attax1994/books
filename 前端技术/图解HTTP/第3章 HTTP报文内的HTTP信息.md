## 第3章 HTTP报文内的HTTP信息

### 3.1 HTTP报文

HTTP报文本身是由多行（用CR+LF作换行符）数据构成的字符串文本。

CR：Carriage Return，回车符，0x0d

LF：Line Feed，换行符，0x0a



### 3.3 编码提升传输速率

编码可以在传输过程中提高传输速率，同时也会消耗更多的CPU资源。

#### 3.3.2 压缩传输的内容编码

内容编码指明应用在实体内容上的编码格式，并保持实体信息原样压缩。

常用的内容编码有：

- gzip（GNU zip）
- compress（UNIX系统的标准压缩）
- deflate（zlib）
- identify（不编码）

#### 3.3.3 分割发送的分块传输编码

把实体主体分块的功能称为分块传输编码（Chunked Transfer Coding）。实体主体的最后一块使用“0(CR+LF)”来标记。



### 3.4 发送多种数据的多部分对象集合

采用MIME（Multipurpose Internet Mail Extensions）机制，容纳多份不同类型的数据。

多部分对象集合包含：

- multipart/form-data：在Web表单文件上传时使用。
- multipart/byteranges：状态码206响应报文包含了多个范围的内容时使用。



### 3.5  获取部分内容的范围请求

使用Header的Range字段来指定资源的byte范围，如`Range: bytes=5001-10000`、`Range: bytes=-3000`和`Range: bytes=5000-`等。