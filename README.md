# WebServer

用C++实现的高性能WEB服务器，经过webbenchh压力测试可以实现QPS:10000+



## 功能

* 利用IO复用技术Epoll与线程池实现多线程的Reactor高并发模型；
* 利用状态机解析HTTP请求报文，实现处理静态资源的请求；

## 环境要求

* Linux
* C++11

## 目录树

```
.
├── bin            可执行文件
│   └── server
├── build        编译的中间代码
├── include       头文件
|   ├── http_conn.h
|   ├── locker.h
|   ├── threadpool.h 
├── resources      静态资源
│   ├── index.html  
│   ├── images 
├── src           源代码
│   ├── http_conn.cpp
│   ├── CMakeLists.txt
│   └── main.cpp
├── test_presure   压力测试         
├── CMakeLists.txt
└── readme.md
```

## 项目编译和启动

1. 在http_conn.cpp第15行修改resources路径（自动获取可能会出错）
2. 在build目录中生成Makefile文件

```
cmake .. 
```

3. 生成可执行文件：

```
make
```

4. 终端启动服务器代码：（端口号可以改）

```
./bin/WebServer 9999
```

5. 浏览器输入:

```
127.0.0.1:9999/index.html
```



## 压力测试

1.编译webbench

```
cd test_presure/webbench-1.5
make
```

2.压力测试

```bash
./webbench -c 100 -t 10 http://127.0.0.1:9999/index.html
./webbench -c 1000 -t 10 http://127.0.0.1:9999/index.html
./webbench -c 5000 -t 10 http://127.0.0.1:9999/index.html
./webbench -c 9000 -t 10 http://127.0.0.1:9999/index.html

//-c 连接数  -t 时间
```

* 测试环境: Ubuntu:18.04虚拟机  4核4G
* 9000+并发数   
* QPS:10000+
