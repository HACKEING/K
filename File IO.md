## open()&openat()
```c++
#include <funcl.h>

int open(const char *path,int oflag,.../* mode_t mode */);
int openat(int fd,const char *path,int oflag,.../* mode_t mode */);

/* Both return:file descriptor if ok,-1 on error */
```
- **The _mode_ parameter is used only when a new fie is being created.**
- **The _oflag_ parameter are mostly:**
	1. **O_RDONLY** - Open for reading only.
	2. **O_WRONLY** - Open for writing only.
	3. **O_RDWR** - Open for reading and writing.
	4. **O_APPEND** - Append to the end of file on each write.
	5. **O_CREAT** Create the file if it doesn't exist.This option requires a third argument.
- **The _fd_ parameter has three possibilities:**
	1. The _path_ parameter specifies an absolute pathname:The _fd_ parameter is ignored and the openat() behaves like open();
	2. The _path_ parameter specifies a relative pathname and the _fd_ parameter is a file descriptor that specifies the starting location in the file system where the relative pathname is to be evaluated;
	3. The _path_ parameter specifies a relative pathname and the _fd_ parameter has the special value AT_FDCWD:The pathname is evaluated starting in the current working directory and the openat() behaves like open();
	

## creat()
```c++
#include <fcntl.h>

int creat(const char *path,mode_t mode);

/* This function is equivalent to: */
open(path,O_WRONLY|O_CREAT|O_TRUNC,mode);

/* If we are creating a temporary file that we wanted to write and then read back,we had to call creat(),close(),and then open().A better way is to use open(),as in: */
open(path,O_RDWR|O_CREAT|O_TRUNC,mode);

/* Return:file descriptor opened for write-only if ok,-1 on error */
```

## close()
```c++
#inlcude <unistd.h>

int close(int fd);

/* Return:0 if ok,-1 on error */
```
- **When a process terminates,all of its open files are closed automatically by the kernel.**

## lseek()
```c++
#include <unistd.h>

off_t lseek(int fd,off_t offset,int whence);

/* To get the current offset: */
off_t currpos=lseek(fd,0,SEEK_CUR);
/* This can also be used to determine if a file is capable of seeking.If fd refers to a pipe/FIFO/socket,lseek() set errno to ESPIPE and returns -1. */

/* Return:new file offset if ok,-1 on error */
```
- **The interpretation of the _offset_ depends on the value of the _whence_ argument:**
	1. **SEEK_SET** - The file's offset is set to offset bytes from the beginning of the file;
	2. **SEEK_CUR** - The file's offset is set to its current value plus the offset.The offset can be positive or negative;
	3. **SEEK_END** - The file's offset is set to the size of the file plus the offset.The offset can be positive or negative;
