## TCP 网络编程的相关数据结构 

### 地址结构：

```cpp
struct sockaddr_in {
    short int sin_family; /* 地址族 */
    unsigned short int sin_port; /* 端口号 */
    struct in_addr sin_addr; /* ip地址 */
    unsigned char sin_zero[8];
};
```
### 上述结构体涉及到的另一个结构体 in_addr 如下：

```cpp
struct in_addr {
    unsigned long s_addr;
};
``` 
## TCP 网络编程各函数的定义

### socket 函数：

```cpp
int socket( int domain, int type,int protocol)
/*
功能：创建一个新的套接字，返回套接字描述符
参数说明：
domain：域类型，指明使用的协议栈，如TCP/IP使用的是PF_INET，其他还有AF_INET6、AF_UNIX
type:指明需要的服务类型, 如
SOCK_DGRAM:数据报服务，UDP协议
SOCK_STREAM:流服务，TCP协议
protocol:一般都取0(由系统根据服务类型选择默认的协议)
*/
```

### bind 函数： 

```cpp
int bind(int sockfd,struct sockaddr* my_addr,int addrlen)
/*
功能：为套接字绑定地址
TCP/IP协议使用sockaddr_in结构，包含IP地址和端口号，服务器使用它来指明熟知的端口号，然后等待连接
参数说明：
sockfd:套接字描述符，指明创建连接的套接字
my_addr:本地地址，IP地址和端口号
addrlen:地址长度
*/
```
### listen 函数： 

```cpp
int listen(int sockfd,int backlog)
/*
功能：
将一个套接字置为监听模式，准备接收传入连接。用于服务器，指明某个套接字连接是被动的监听状态。
参数说明：
Sockfd:套接字描述符，指明创建连接的套接字
backlog: linux内核2.2之前，backlog参数=半连接队列长度+已连接队列长度；linux内核2.2之后，backlog参数=已连接队列（Accept队列）长度
*/
```

### accept 函数： 

```cpp
int accept(int sockfd, structsockaddr *addr, int *addrlen)
/*
功能：从已完成连接队列中取出成功建立连接的套接字，返回成功连接的套接字描述符。
参数说明：
Sockfd:套接字描述符，指明正在监听的套接字
addr:提出连接请求的主机地址
addrlen:地址长度
*/
``` 

### send 函数：

```cpp
int send(int sockfd, const void * data, int data_len, unsigned int flags)
/*
功能：在TCP连接上发送数据,返回成功传送数据的长度，出错时返回－1。send会将数据移到发送缓冲区中。
参数说明：
sockfd:套接字描述符
data:指向要发送数据的指针
data_len:数据长度
flags:通常为0
*/
``` 
### recv 函数： 

```cpp
int recv(int sockfd, void *buf, intbuf_len,unsigned int flags)
/*
功能：接收数据,返回实际接收的数据长度，出错时返回－1。
参数说明：
Sockfd:套接字描述符
Buf:指向内存块的指针
Buf_len:内存块大小，以字节为单位
flags:一般为0
*/
```  

### close 函数：  

```cpp
close(int sockfd)
/*
功能：撤销套接字。如果只有一个进程使用，立即终止连接并撤销该套接字，如果多个进程共享该套接字，将引用数减一，如果引用数降到零，则关闭连接并撤销套接字。
参数说明：
sockfd:套接字描述符
*/ 
```  

### connect 函数：

```cpp
int connect(int sockfd,structsockaddr *server_addr,int sockaddr_len)
/*
功能： 同远程服务器建立主动连接，成功时返回0，若连接失败返回－1。
参数说明：
Sockfd:套接字描述符，指明创建连接的套接字
Server_addr:指明远程端点：IP地址和端口号
sockaddr_len :地址长度
*/
```
