**4. Signals (****`kill`****,** **`signal`****)**

- Define signal types:
c
Copy code



```
typedef void (*signal_handler_t)(int);
void signal(int sig, signal_handler_t handler);
void kill(int pid, int sig);
```




- Dispatch signals during task execution using a signal stack.


