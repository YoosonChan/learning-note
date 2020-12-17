# [```Websocket```](https://www.cnblogs.com/llljpf/p/10830651.html)
## WebSocket的定义

　　```WebSocket```是```html5```提供的一种在单个```TCP```连接上进行双向通信的协议，解决了客户端和服务端之间的实时通信问题。浏览器和服务器只需完成一次握手，两者之间就可以创建一个持久性的```TCP```连接，此后服务器和客户端通过此```TCP```连接进行双向实时通信。

## WebSocket的优点

　　很多网站为了实现数据推送，所用的技术都是```ajax轮询```。轮询是在特定的时间间隔，由浏览器主动发起请求，将服务器的数据拉回来。轮询需要不断的向服务器发送请求，会占用很多带宽和服务器资源。```WebSocket```建立```TCP```连接后，服务器可以主动给客户端传递数据，能够更好的节省服务器资源和带宽，实现更实时的数据通讯。

![](https://img2018.cnblogs.com/blog/1038427/201905/1038427-20190508104500965-1818149905.png)

## WebSocke的属性

![](https://img2018.cnblogs.com/blog/1038427/201905/1038427-20190508105407065-1003003903.png)

## WebSocket的方法

![](https://img2018.cnblogs.com/blog/1038427/201905/1038427-20190508105515191-1373394332.png)

## WebSocket的实例

　　```WebSocket```协议本质上是一个基于```TCP```的协议，为了建立一个```WebSocket```连接，浏览器需要向服务器发起一个```HTTP```请求，这个请求和普通的```HTTP```请求不同，它包含了一些附加头信息，服务器解析这些附加头信息后产生应答信息返回给客户端，客户端和服务端的```WebSocket```连接就建立起来了，双方可以通过连接通道自由的传递信息，并且这个连接会持续存在直到客户端或服务端某一方主动关闭连接。

```js
function webSocket(){
　　if("WebSocket" in window){
　　　　console.log("您的浏览器支持WebSocket");
　　　　var ws = new WebSocket("ws://localhost:8080"); //创建WebSocket连接
　　　　//...
　　}else{
　　　　console.log("您的浏览器不支持WebSocket");
　　}
}
```

# WebSocket的事件

　　客户端支持```WebSocket```的浏览器中，在创建```socket```后，可以通过```onopen```、```onmessage```、```onclose```和```onerror```四个事件对```socket```进行响应。```WebSocket```的所有操作都是采用事件的方式触发的，这样不会阻塞```UI```，是的```UI```有更快的响应时间，有更好的用户体验。

　　浏览器通过```Javascript```向服务器发出建立```WebSocket```连接的请求，连接建立后，客户端和服务器就可以通过```TCP```连接直接交换数据。当你获取```WebSocket```连接后，可以通多```send()```方法向服务器发送数据，可以通过```onmessage```事件接收服务器返回的数据。

```js
var ws = new WebSocket("ws://localhost:8080"); 
//申请一个WebSocket对象，参数是服务端地址，同http协议使用http://开头一样，WebSocket协议的url使用ws://开头，另外安全的WebSocket协议使用wss://开头
ws.onopen = function(){
　　//当WebSocket创建成功时，触发onopen事件
   console.log("open");
　　ws.send("hello"); //将消息发送到服务端
}
ws.onmessage = function(e){
　　//当客户端收到服务端发来的消息时，触发onmessage事件，参数e.data包含server传递过来的数据
　　console.log(e.data);
}
ws.onclose = function(e){
　　//当客户端收到服务端发送的关闭连接请求时，触发onclose事件
　　console.log("close");
}
ws.onerror = function(e){
　　//如果出现连接、处理、接收、发送数据失败的时候触发onerror事件
　　console.log(error);
}
```
