
#### 3. **Helper Functions**

##### **`waitdisk()`**
Waits for the disk to be ready for operations:
c
Copy code


`while((inb(0x1F7) & 0xC0) != 0x40);`


- Reads the disk status register (port `0x1F7`).
- Waits until the disk is ready (`0x40`).


##### **`readsect(void *dst, uint offset)`**
Reads a single disk sector into the destination address:
c
Copy code



```
waitdisk(); // Wait for disk readiness
outb(0x1F2, 1); // Sector count = 1
outb(0x1F3, offset); // Set sector offset (low byte)
outb(0x1F7, 0x20); // Command: Read sector
waitdisk(); // Wait for operation to complete
insl(0x1F0, dst, SECTSIZE/4); // Copy data into destination

```



##### **`readseg(uchar* pa, uint count, uint offset)`**
Reads multiple bytes (spanning sectors) into memory:
c
Copy code



```
epa = pa + count; // End pointer
pa -= offset % SECTSIZE; // Align to sector boundary
offset = (offset / SECTSIZE) + 1; // Start sector at offset 1

for(; pa < epa; pa += SECTSIZE, offset++)
    readsect(pa, offset); // Read each sector

```


- Aligns the address to sector boundaries.
- Reads data sector by sector into the specified memory region.


### **Workflow Overview**
1. **Search for Multiboot Header:**
- Load the first 8192 bytes of the kernel to locate the Multiboot header.


- **Validate the Multiboot Header:**
- Ensure the header is valid using the magic number, checksum, and flags.


- **Load the Kernel:**
- Use the `load_addr` and `load_end_addr` fields to load the kernel into memory.


- **Zero-Out the BSS:**
- Ensure the BSS segment is initialized to zero.


- **Jump to Kernel:**
- Transfer control to the kernel's entry point specified in `entry_addr`.

	