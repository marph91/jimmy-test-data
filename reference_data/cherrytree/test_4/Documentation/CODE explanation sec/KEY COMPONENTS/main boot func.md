
#### **Main Boot Function (****`bootmain`****)**
The main function of the bootloader loads the kernel and transfers execution to the kernel's entry point.
**Steps in** **`bootmain()`****:**
1. **Scratch Space and Multiboot Header Search:**
c
Copy code



```
x = (uint32*) 0x10000; // Use address 0x10000 as temporary storage
readseg((uchar*)x, 8192, 0); // Read the first 8192 bytes (16 sectors) from disk

```


- The Multiboot header must be within the first 8192 bytes of the kernel.
- The `readseg` function loads this segment into memory for inspection.


- **Identify the Multiboot Header:**
c
Copy code



```
for (n = 0; n < 8192/4; n++) {
    if (x[n] == 0x1BADB002) // Check for Multiboot magic number
        if ((x[n] + x[n+1] + x[n+2]) == 0) // Verify checksum
            goto found_it;
}

```


- The loop scans the loaded segment for the **Multiboot magic number** (`0x1BADB002`).
- It also verifies the checksum to ensure the header is valid.


- **Handle Invalid Header:** If the header is not found, the bootloader exits:
c
Copy code


`return;`



- **Process the Multiboot Header:**
c
Copy code



```
hdr = (struct mbheader *) (x + n); // Pointer to the Multiboot header

if (!(hdr->flags & 0x10000))
    return; // The header lacks load fields; cannot proceed
if (hdr->load_addr > hdr->header_addr)
    return; // Invalid addresses
if (hdr->load_end_addr < hdr->load_addr)
    return; // Invalid range

```


- The header's fields are validated to ensure the kernel can be loaded.


- **Load the Kernel into Memory:**
c
Copy code



```
readseg((uchar*) hdr->load_addr,
        (hdr->load_end_addr - hdr->load_addr),
        (n * 4) - (hdr->header_addr - hdr->load_addr));

```


- The `readseg` function is called to load the kernel from disk into memory.


- **Zero-Out BSS Segment:**
c
Copy code



```
if (hdr->bss_end_addr > hdr->load_end_addr)
    stosb((void*) hdr->load_end_addr, 0,
          hdr->bss_end_addr - hdr->load_end_addr);

```


- The BSS (uninitialized data) segment is zeroed out using `stosb`.


- **Jump to Kernel Entry Point:**
c
Copy code



```
entry = (void(*)(void))(hdr->entry_addr);
entry(); // Transfer control to the kernel

```


- The bootloader jumps to the kernel's entry point, effectively handing over control to the kernel.


