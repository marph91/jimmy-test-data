**File System Operations (****`open`****,** **`read`****,** **`write`****)**
- Create a Virtual File System (VFS) layer:c
Copy code



```
typedef struct file {
    char *name;
    uint64_t size;
    void *data;
} file_t;

int open(const char *path);
int read(int fd, void *buffer, size_t size);
int write(int fd, const void *buffer, size_t size);
```




