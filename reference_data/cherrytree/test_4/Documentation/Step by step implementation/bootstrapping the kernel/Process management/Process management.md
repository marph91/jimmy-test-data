**2. Process Management (****`fork`****,** **`exec`****)**
- Define a basic task structure:
c
Copy code



```
typedef struct task {
    int pid;
    uint64_t *stack;
    struct task *next;
} task_t;

```



- Implement `fork` by duplicating the current task:
c
Copy code



```
int fork() {
    task_t *new_task = allocate_task();
    copy_memory(new_task->stack, current_task->stack, STACK_SIZE);
    return new_task->pid;
}

```



- Implement `exec` by replacing the task's memory:
c
Copy code



```
int exec(const char *path) {
    load_program(path, current_task->stack);
    return 0; // Success
}
```




