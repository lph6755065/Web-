# TCP 网络编程的相关数据结构 

## 地址结构：
```cpp
struct sockaddr_in {
    short int sin_family; /* 地址族 */
    unsigned short int sin_port; /* 端口号 */
    struct in_addr sin_addr; /* ip地址 */
    unsigned char sin_zero[8];
};
```
