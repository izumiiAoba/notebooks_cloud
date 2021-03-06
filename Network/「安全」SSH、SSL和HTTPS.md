1. [密码学笔记 - ruanyifeng.com](http://www.ruanyifeng.com/blog/2006/12/notes_on_cryptography.html)
2. [公钥，私钥和数字签名这样最好理解 - CSDN](https://blog.csdn.net/21aspnet/article/details/7249401)
3. [HTTPS原理全解析 - bilibili](https://www.bilibili.com/video/BV1w4411m7GL)

## 加密

### 加密方法

- 单钥加密`private key cryptography`
  - 对称加密/共享密钥加密
  - 加密和解密过程都用同一套密码
- 双钥加密`public key cryptography`
  - 非对称加密/公开公钥加密
  - 加密和解密过程用的是两套密码（公钥、私钥）

### 双钥加密

- `公钥`和`私钥`是**一一对应**的关系，有一把公钥就必然有一把与之对应的、独一无二的私钥，反之亦成立。
- `公钥`和`私钥`是成对的，它们**互相解密**。
  - 公钥加密 => 私钥解密
  - 私钥数字签名 => 公钥验证
- `非对称加密`的**计算量**会比`对称加密`的大

### 数字签名

- [数字签名 - ruanyifeng.com](http://www.ruanyifeng.com/blog/2011/08/what_is_a_digital_signature.html)

- 对内容做一次数字`摘要`，将摘要结果用`私钥`加密作数字签名，数字签名和内容一并发送
- 收方用`公钥`对数字签名作验证，得到数字签名里的摘要结果。对**收到的内容**做一次数字摘要，以此与数字签名中的摘要结果作**比较**，可验证内容是否被修改。

### 数字证书

- 通过第三方**证书中心CA**`certificate authority`为公钥作认证
- CA用**自己的私钥**，对用户的公钥和一些相关信息加密，生成数字证书`Digital Certificate`

- 数字证书同数字签名和内容一并发送
- 收方用**CA的公钥**解开数字证书，得到用户的公钥 ...

## SSH

- SSH是创建在`应用层`和`传输层`基础上的安全协议，为计算机上的Shell（壳层）提供安全的传输和使用环境
- 通俗点讲就是只有`SSH客户端`，和`SSH服务器`之间的通信才能使用这个协议，其他软件服务**无法使用**它
- 如果要在Windows系统中使用SSH，会用到`PuTTY`

## HTTPS

### HTTP的不足

- 通信使用明文（不加密），内容可能会被窃听
- 不验证通信方的身份，因此有可能遭遇伪装
- 无法证明报文的完整性，所以有可能已遭篡改

### 明文传输

- 等同裸奔

### 对称加密

- 密钥 k
- Server 不可能为每一个 Client 创建一个 k
- 黑客是可以充当成一个 Client，所以也能获取 k

### 非对称加密

- 公钥 pk：所有人都能拿到
- 私钥 sk：Server持有
- 黑客仍旧能充当 Client 获取 pk，因此 Server => Client 是不安全的
- 黑客无法获取 sk，Client => Server 是安全的

### 非对称加密 + 对称加密

- 思路
  - 通过`非对称加密`，协商出临时的 k
  - 再通过 k 使用`对称加密`，传输数据

- 协商出的 k，每个 Client 都有一个

- 缺陷：中间人攻击

  Client 第一次请求 pk 时，无法知道 pk 是来自服务器，还是来自黑客

### 非对称加密 + 对称加密 + CA

- 证书颁发机构，**C**ertificate **A**uthority

- 思路

  - Server 将自己的 pk 转给`CA`获得`License`= func(**csk**,pk)
  - Client 收到 Server 传来的 License，通过 Client **内置**在浏览器的很多 cpk 解密 License 得到 pk

  - ... ...

## SSL/TLS 握手过程

- 安全地协商出一份对称加密的`密钥 MasterSecret` 

![](../_images/image-20200712221742723.png)

1. ClientHello
   - 客户端通过发送 Client Hello 报文开始 SSL通信
   - 其中包含客户端生成的随机数`Random1`/**ClientRandom**
2. ServerHello
   - 服务器生成的随机数`Random2`/**ServerRandom**
3. Certificate
   - Server下发自己的License
   - License中包含服务器上的公钥pk
4. ServerHelloDone
   - 最初阶段的SSL握手协商**部分**结束

5. ClientKeyExchange (Client)
   - 用（3）中得到的服务器公钥 pk，加密`Random3` => **PreMaster Secret**
   - 将 PreMaster Secret 发送给服务器
6. Change Cipher Spec
   - 报文会提示服务器，在此报文之后的通信会采用 PreMaster Secret 密钥加密

7. Handshake:Finished (Client)
8. Change Cipher Spec (Server)
9. Handshake:Finished (Server)

> Master Secret = f(Random1, Random2, PreMaster Secret)

