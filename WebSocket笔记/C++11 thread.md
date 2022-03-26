## C++11 线程库

### 基本使用  

需要引入头文件：

```cpp
#include<thread>
```

创建一个新线程来执行 run 函数：

```cpp
thread t(run);  //实例化一个线程对象t，让该线程执行run函数，构造对象后线程就开始执行了
```

假如说 run 函数需要传入参数 a 和 b，我们可以这样构造： 

```cpp
thread t(run,a,b);  //实例化一个线程对象t，让该线程执行run函数，传入a和b作为run的参数
``` 

**需要注意的是，传入的函数必须是全局函数或者静态函数，不能是类的普通成员函数。  

join 函数会阻塞主线程，直到 join 函数的 thread 对象标识的线程执行完毕为止，join 函数使用方法如下：

```cpp
t.join(); //调用join后，主线程会一直阻塞，直到子线程的run函数执行完毕.
```

但有时候我们需要主线程在继续完成其它的任务，而不是一直等待子线程结束，这时候我们可以使用 detach 函数。

detach 函数会让子线程变为分离状态，主线程不会再阻塞等待子线程结束，而是让系统在子线程结束时自动回收资源。使用的方法如下：

```cpp
t.detach();
```  
### 代码示例  

接下来用一段代码来示范如何进行简单的多线程编程，我们构建两个线程，同时输出 1-10，如下：

新建一个文件名为 test_thread.cpp：

```cpp
#include <iostream>
#include <thread>
#include <unistd.h>
using namespace std;
void print(){
    for(int i=1;i<=10;i++){
        cout<<i<<endl;
        sleep(1);   //休眠1秒钟
    }
}
int main(){
    thread t1(print),t2(print);
    t1.join();
    t2.join();
    //也可以使用detach
    //t1.detach();
    //t2.detach();
}
```

然后使用 g++ 进行编译，需要注意的是这里要用上 -l 来链接线程动态库，如下：

```cpp
g++ -o test_thread test_thread.cpp -lpthread
```  

