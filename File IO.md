### open()&openat()
```c++
#include <funcl.h>

int open(const char *path,int oflag,.../*mode_t mode*/);
int openat(int fd,const char *path,int oflag,.../*mode_t mode*/);
```
* **mode仅当创建新文件时才使用，用于指定所创建文件的访问权限；**
* **oflag为以下常量，或其或运算（|）结果：**
  * O_RDONLY:以只读模式打开；
  * O_WRONLY:以只写模式打开；
  * O_RDWR:以读写模式打开；
  * O_EXEC:以只执行模式打开；
  * O_SEARCH:以只搜索模式打开（应用于目录）；
  * **以上5个常量必须指定，且只能指定其中一项；以下常量则是可选的；**
  * O_APPEND:每次写时，都追加到文件尾端；
  * O_CLOEXEC:把FD_CLOEXEC设置为文件描述符标志；
  * O_CREAT:若文件不存在，则创建该文件。使用该选项时需指定mode参数；
  * O_DRECTORY:如果path引用的不是目录，则出错；
  * O_EXCL:如果同时指定了O_CREAT，且文件已存在，则出错。可以此检测文件是否存在；
  * O_NOCTTY:如果path引用的是终端设备，则不将该设备分配作为此进程的控制终端；
  * O_NOFOLLOW:如果path引用的是一个符号链接，则出错；
  * O_NONBLOCK:如果path引用的是一个FIFO／块特殊文件／字符特殊文件，则
