
#### **How Will We Build It?**
- **Step 1: Planning the Kernel**
- Define the **scope of POSIX compliance** (basic syscalls vs full compliance).
- Choose programming languages:- **C:** Primary language for portability and compliance.
- **Assembly:** For low-level tasks like context switching.


- Set up a **development environment**:- Compiler: `gcc` or `clang`.
- Debugger: `gdb`.
- Emulator: `QEMU`.




- **Step 2: Bootstrapping**
- Write a minimal bootloader (e.g., GRUB with Multiboot2..
- Create an entry point for the kernel in assembly.
- Initialize the stack and transition to C code.


- **Step 3: Implement POSIX Core Features**
- **Processes:** Implement `fork()`, `exec()`, and `wait()` using task structures and a simple scheduler.
- **File System:** Add a Virtual File System (VFS) layer with basic operations (`open`, `read`, `write`).
- **Signals:** Implement signal handling mechanisms.
- **IPC:** Add pipes and shared memory management.


- **Step 4: Debugging and Testing**
- Use POSIX-compliant programs to test functionality (e.g., a basic shell).
- Debug with tools like `gdb` in the QEMU environment



