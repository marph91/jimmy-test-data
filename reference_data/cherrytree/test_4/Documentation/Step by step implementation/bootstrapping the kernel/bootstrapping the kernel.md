**1. Bootstrapping the Kernel**
- Write a Multiboot2 header for GRUB compatibility.

- Transition from assembly to C:
asm
Copy code



```
section .text
global start
start:
    cli                 ; Disable interrupts
    mov esp, 0x90000    ; Set up stack
    call kernel_main    ; Jump to C code
    hlt                 ; Halt if we return

```



- Initialize the kernel:
c
Copy code



```
void kernel_main() {
    init_gdt();         // Set up Global Descriptor Table
    init_interrupts();  // Initialize the Interrupt Descriptor Table
    init_memory();      // Set up paging and memory management
}
```




