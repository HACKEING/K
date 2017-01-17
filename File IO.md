## open()&openat()
```c++
#include <funcl.h>

int open(const char *path,int oflag,.../* mode_t mode */);
int openat(int fd,const char *path,int oflag,.../* mode_t mode */);

/* Both return:file descriptor if ok,-1 on error */
```
**The last argument (mode) is used only when a new fie is being created.**	
**The oflag argument are mostly:**	
* O_RDONLY	Open for reading only	
* O_WRONLY	Open for writing only	
* O_RDWR	Open for reading and writing	

---

## create()
