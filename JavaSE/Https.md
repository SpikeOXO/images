http：	超文本传输协议

协议:	规定了客户端和服务端之间的通信规范

1，http协议是工作在tpc/ip模型的应用层

2，http协议是基于请求和响应模式

3，http协议是短链接

4，http协议是明文传输

5，http协议是无状态

无状态：客户端>服务端>数据库;账号验证

客户端>服务端

服务端，验证客户端x账号正确

客户端，再次向服务端请求服务端不知客户端是谁

有状态：服务端会向登陆过的客户端发出一个标识，下次登录不用去数据库验证账号

应用层	http

传输层	tcp/udp

网络层	ip

数据链路层

http1.0：用到http协议的时候建立tcp连接，发送完毕之后断开tcp连接

http1.1：用到http协议的时候建立tcp连接，发送完毕之后在一段时间内保存连接

http1.1 是针对tcp来说的长连接	是tcp的长连接，不是http

http协议

请求：

1，请求行信息

请求方式		地址			版本

GET  		index.html   	http/1.1

post  		index.html   	http/1.1

2，请求头信息

   对应：key	=	value

accept；请求的格式

aceept-encoding；请求压缩格式

aceept-language；

cahe-control；缓存

cookie；

user-agent；请求设备标识

3，请求行正文

GET请求是没有正文

GET请求如果向服务器发送数据，数据是通过请求行信息的请求地址带过去，

举例：

GET   index.html?username=name&password=123   http/1.1

POST

响应：

1，响应行信息

协议及版本	状态码	描述

HTTP/1.1		404		客户端问题（未找到网页）

   5xx	   服务器问题

   2xx	   ok

2，响应头信息

content-length

压缩方式

时间戳

3，响应行正文

真正的内容                                                                                               