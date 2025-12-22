 **IPC (Pipes and Shared Memory)**
- Implement pipes:
c
Copy code



```
int pipe(int fds[2]) {
    create_pipe(fds);
    return 0;
}
```




- Add shared memory regions for communication:
c
Copy code


`void *shmget(int key, size_t size);`




