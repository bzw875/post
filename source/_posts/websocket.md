---
title: WebSocket协议介绍
date: 2020-08-27 14:45:03
updated: 2020-08-27 14:45:03
tags: 网络
categories:
---

# WebSocket协议

## 一、内容概览
WebSocket的出现，使得浏览器具备了实时双向通信的能力。

## 二、什么是WebSocket
HTML5开始提供的一种浏览器与服务器进行全双工通讯的网络技术，属于应用层协议。它基于TCP传输协议，并复用HTTP的握手通道。

对大部分web开发者来说，上面这段描述有点枯燥，其实只要记住几点：

* WebSocket可以在浏览器里使用
* 支持双向通信
* 使用很简单

#### 1、有哪些优点
说到优点，这里的对比参照物是HTTP协议，概括地说就是：支持双向通信，更灵活，更高效，可扩展性更好。

* 支持双向通信，实时性更强。
* 更好的二进制支持。
* 较少的控制开销。连接创建后，ws客户端、服务端进行数据交换时，协议控制的数据包头部较小。在不包含头部的情况下，服务端到客户端的包头只有2~10字节（取决于数据包长度），客户端到服务端的的话，需要加上额外的4字节的掩码。而HTTP协议每次通信都需要携带完整的头部。
* 支持扩展。ws协议定义了扩展，用户可以扩展协议，或者实现自定义的子协议。（比如支持自定义压缩算法等）
对于后面两点，没有研究过WebSocket协议规范的同学可能理解起来不够直观，但不影响对WebSocket的学习和使用。



## 三、入门例子
在正式介绍协议细节前，先来看一个简单的例子，有个直观感受。例子包括了WebSocket服务端、WebSocket客户端（网页端）。完整代码可以在 这里 找到。

这里服务端用了ws这个库。相比大家熟悉的socket.io，ws实现更轻量，更适合学习的目的。

#### 1、服务端
代码如下，监听8080端口。当有新的连接请求到达时，打印日志，同时向客户端发送消息。当收到到来自客户端的消息时，同样打印日志。
``` javascript
var app = require('express')();
var server = require('http').Server(app);
var WebSocket = require('ws');

var wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', function connection(ws) {
    console.log('server: receive connection.');
    
    ws.on('message', function incoming(message) {
        console.log('server: received: %s', message);
    });

    ws.send('world');
});

app.get('/', function (req, res) {
  res.sendfile(__dirname + '/index.html');
});

app.listen(3000);
```
#### 2、客户端
代码如下，向8080端口发起WebSocket连接。连接建立后，打印日志，同时向服务端发送消息。接收到来自服务端的消息后，同样打印日志。
``` javascript
  var ws = new WebSocket('ws://localhost:8080');
  ws.onopen = function () {
    console.log('ws onopen');
    ws.send('from client: hello');
  };
  ws.onmessage = function (e) {
    console.log('ws onmessage');
    console.log('from server: ' + e.data);
  };

```
#### 3、运行结果
可分别查看服务端、客户端的日志，这里不展开。

``` bash
服务端输出：

server: receive connection.
server: received hello
客户端输出：

client: ws connection is open
client: received world
```
## 四、如何建立连接
前面提到，WebSocket复用了HTTP的握手通道。具体指的是，客户端通过HTTP请求与WebSocket服务端协商升级协议。协议升级完成后，后续的数据交换则遵照WebSocket的协议。

#### 1、客户端：申请协议升级
首先，客户端发起协议升级请求。可以看到，采用的是标准的HTTP报文格式，且只支持GET方法。
```
GET / HTTP/1.1
Host: localhost:8080
Origin: http://127.0.0.1:3000
Connection: Upgrade
Upgrade: websocket
Sec-WebSocket-Version: 13
Sec-WebSocket-Key: w4v7O6xFTi36lq3RNcgctw==
```
重点请求首部意义如下：

* Connection: Upgrade：表示要升级协议
* Upgrade: websocket：表示要升级到websocket协议。
* Sec-WebSocket-Version: 13：表示websocket的版本。如果服务端不支持该版本，需要返回一个Sec-WebSocket-Versionheader，里面包含服务端支持的版本号。
* Sec-WebSocket-Key：与后面服务端响应首部的Sec-WebSocket-Accept是配套的，提供基本的防护，比如恶意的连接，或者无意的连接。

> 注意，上面请求省略了部分非重点请求首部。由于是标准的HTTP请求，类似Host、Origin、Cookie等请求首部会照常发送。在握手阶段，可以通过相关请求首部进行 安全限制、权限校验等。

#### 2、服务端：响应协议升级
服务端返回内容如下，状态代码101表示协议切换。到此完成协议升级，后续的数据交互都按照新的协议来。

```
HTTP/1.1 101 Switching Protocols
Connection:Upgrade
Upgrade: websocket
Sec-WebSocket-Accept: Oy4NRAQ13jhfONC7bP8dTKb4PTU=
```

> 备注：每个header都以\\r\\n结尾，并且最后一行加上一个额外的空行\\r\\n。此外，服务端回应的HTTP状态码只能在握手阶段使用。过了握手阶段后，就只能采用特定的错误码。

#### 3、Sec-WebSocket-Accept的计算
Sec-WebSocket-Accept根据客户端请求首部的Sec-WebSocket-Key计算出来。

计算公式为：

将Sec-WebSocket-Key跟258EAFA5-E914-47DA-95CA-C5AB0DC85B11拼接。
通过SHA1计算出摘要，并转成base64字符串。
伪代码如下：

>toBase64( sha1( Sec-WebSocket-Key + 258EAFA5-E914-47DA-95CA-C5AB0DC85B11 )  )
验证下前面的返回结果：

``` javascript
const crypto = require('crypto');
const magic = '258EAFA5-E914-47DA-95CA-C5AB0DC85B11';
const secWebSocketKey = 'w4v7O6xFTi36lq3RNcgctw==';

let secWebSocketAccept = crypto.createHash('sha1')
    .update(secWebSocketKey + magic)
    .digest('base64');

console.log(secWebSocketAccept);
// Oy4NRAQ13jhfONC7bP8dTKb4PTU=
```