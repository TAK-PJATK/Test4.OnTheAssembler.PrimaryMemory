# Notes

## Logical Addresses (Virtual Addresses)

Logical addresses, also known as virtual addresses, are used by programs during execution.

They represent memory locations within a process’s address space.

The programmer (or compiler) treats the logical addresses as if the first memory cell has address 0.

The entire area of RAM assigned to the process appears contiguous from the program’s perspective.

Logical addresses provide an abstraction layer, allowing programs to interact with memory without worrying about the actual physical locations.

The operating system handles the translation of logical addresses to physical addresses.

This abstraction enables features like memory protection and process isolation.

## Contiguous Memory Space

When a process is allocated memory, its logical address space is considered contiguous.

Contiguous memory means that the addresses are consecutive and follow a linear order.

The program can access data structures, variables, and code using these logical addresses.

However, the actual physical memory may not be contiguous; the OS manages the mapping.

## Memory Management Unit (MMU)

The MMU translates logical addresses to physical addresses.

It maintains a mapping table (page table) that associates logical pages with physical frames.

When the program accesses a logical address, the MMU performs the translation.

The MMU ensures memory protection, preventing unauthorized access to other processes’ memory.

In summary, logical addresses provide an abstract view of memory for programs, allowing them to operate independently of the underlying hardware. The OS and MMU handle the translation to physical addresses, ensuring efficient and secure memory management.

# [DDR SDRAM](https://sl.bing.net/cn4ujklsBEW)

## Random-Access Memory (RAM)

RAM allows data to be accessed in an arbitrary (random) order.

Unlike sequential access memory (where data must be read in a specific order), RAM provides flexibility for quick data retrieval.

It serves as the primary working memory for computers, storing data that the CPU actively uses during program execution.

### Dynamic

The term “dynamic” refers to the need for periodic refreshing of memory content.

In DRAM, each memory cell stores charge in a capacitor. Over time, this charge leaks away, so the memory controller must read and rewrite the data periodically to maintain its integrity.

Dynamic memory is more space-efficient but requires additional circuitry for refreshing.

### Synchronous

Synchronous memory (SDRAM) synchronizes memory access with the system clock.

Data transfers occur at specific clock cycles, simplifying timing and allowing higher frequencies.
SDRAM modules are commonly used in computers, servers, and other devices.

### Double Data Rate (DDR)

DDR memory sends data twice per clock cycle (both on the rising and falling edges of the clock signal).

This effectively doubles the data transfer rate compared to single data rate (SDR) memory.
DDR SDRAM is widely used due to its improved bandwidth and efficiency.

### Interleaving

Interleaving is a technique used to enhance memory performance by allowing multiple read or write operations to occur simultaneously.

In interleaved memory, memory banks are divided into smaller units called **interleaves**.

When a memory request occurs, the system can access data from different interleaves in parallel.

Interleaving improves memory bandwidth and reduces latency, especially in multi-core systems or servers.

For example, dual-channel or quad-channel memory configurations use
interleaving to boost performance.

### Returning Data in Multi-Byte Chunks

SDRAM typically returns data in chunks, often referred to as **burst mode**.

Burst mode allows the memory controller to fetch multiple contiguous data words in a single operation.

When one memory cell is accessed, its neighboring cells are also fetched, anticipating future requests.

Burst transfers improve overall memory throughput and efficiency.

The burst length (number of data words fetched in one operation) varies based on the specific SDRAM type (e.g., burst length of 4, 8, or more).

## Paging

### Multilevel Paging

**Multilevel Paging** is a **paging scheme** that involves two or more levels of page tables arranged in a hierarchical manner. It's also known as **hierarchical paging**. Let's delve into the details:

1. **Why Multilevel Paging?**
   - Consider a 32-bit physical address space with a page size of **4KB**.
   - If we have **1 million** entries in the page table (since 32 bits allow for 2^20 entries), the page table size would be **3MB**.
   - Each process has its own page table, leading to significant memory wastage just for storing page tables.
   - **Multilevel paging** addresses this issue by using a hierarchical structure, where only the outermost page table resides in main memory, and other page tables are brought in as needed.

2. **Levels in Multilevel Paging:**
   - Regardless of the number of levels, all page tables are stored in main memory.
   - Each level requires a memory access to get the physical address of the page frame.
   - Each page table entry (except the last level) contains the base address of the next level page table.

3. **Example of a 3-Level Paging System:**
   - Let's illustrate this with a 3-level paging system.
   - The virtual address consists of three parts:
     - **Level 1 Offset**: Present in the virtual address.
     - **Level 2 Offset**: Present in the virtual address.
     - **Level 3 Offset**: Present in the virtual address.
   - The actual page frame address is obtained from the last level page table entry.

4. **Important Formulas:**
   - Number of entries in a page table:
     - \( \text{{Number of entries}} = \frac{{\text{{virtual address space size}}}}{{\text{{page size}}}} \)
   - Virtual Address Space Size:
     - \( \text{{Virtual Address Space Size}} = 2^n \) (where \( n \) is the number of bits used to represent the virtual address)
   - Size of Page Table:
     - \( \text{{Size of Page Table}} = \text{{number of entries in page table}} \times \text{{size of PTE}} \)
     - If the page table size exceeds the desired size, create one more level.

5. **Advantages of Multilevel Paging:**
   - **Reduced Memory Overhead**: With fewer entries per level, less memory is needed to store the page table.
   - **Faster Page Table Lookup**: Smaller page tables mean quicker lookups.

Remember, multilevel paging optimizes memory usage and enhances efficiency in managing page tables! 🚀📚

Sources:

1. [GeeksforGeeks: Multilevel Paging in Operating System](https://www.geeksforgeeks.org/multilevel-paging-in-operating-system/)
2. [Gate Vidyalay: Multilevel Paging in OS](https://www.gatevidyalay.com/multilevel-paging-paging-in-operating-system/) ¹²

Source: Conversation with Bing, 16/05/2024
(1) Multilevel Paging in Operating System - GeeksforGeeks. <https://www.geeksforgeeks.org/multilevel-paging-in-operating-system/>.
(2) Multilevel Paging in OS | Paging in OS | Gate Vidyalay. <https://www.gatevidyalay.com/multilevel-paging-paging-in-operating-system/>.
(3) Two Level Paging and Multi Level Paging in OS - GeeksforGeeks. <https://www.geeksforgeeks.org/two-level-paging-and-multi-level-paging-in-os/>.

### Why 32 bits allow for 2*20 entries?

The reason why a 32-bit address space allows for \( 2^{20} \) entries in a page table is due to the division of the address space by the page size. Here's a breakdown of the concept:

1. **Address Space**: A 32-bit address space means that each address can be 32 bits long, allowing for \( 2^{32} \) unique addresses.
2. **Page Size**: If the page size is 4 KB (which is \( 2^{12} \) bytes), then each page can be uniquely identified with \( 2^{12} \) different addresses.
3. **Page Table Entries**: To map the entire address space to pages, you divide the total number of addresses by the number of addresses per page:
   $$ \text{Number of Page Table Entries} = \frac{2^{32}}{2^{12}} = 2^{20} $$

This calculation shows that with a 32-bit address space and a 4 KB page size, you would need \( 2^{20} \) entries in the page table to cover the entire address space. Each entry corresponds to one page of memory. The result is that the page table can become quite large, which is why multilevel paging is used to manage this efficiently¹.

Source: Conversation with Bing, 16/05/2024
(1) memory management - Calculating Page Table Size - Stack Overflow. <https://stackoverflow.com/questions/16323890/calculating-page-table-size>.
(2) Page Table Entries in Page Table - GeeksforGeeks. <https://www.geeksforgeeks.org/page-table-entries-in-page-table/>.
(3) Why does Page Directory entries need 20 bits to point 2^10 Page Tables?. <https://stackoverflow.com/questions/26858196/why-does-page-directory-entries-need-20-bits-to-point-210-page-tables>.
(4) How Do Multi-Level Page Tables Save Memory Space? - Baeldung. <https://www.baeldung.com/cs/multi-level-page-tables>.
(5) en.wikipedia.org. <https://en.wikipedia.org/wiki/Page_table>.

Consider a machine with 64 MB physical memory and a 32-bit virtual address space. If the page size is 4KB, what is the approximate size of the page table?

(A) 16 MB

(B) 8 MB

(C) 2 MB

(D) 24 MB

Answer (C)

Explanation
Physical Address Space = 64MB = 226B
Virtual Address = 32-bits,  ∴ Virtual Address Space = 232B
Page Size = 4KB = 212B
Number of pages = 232/212 = 220 pages.

Number of frames = 226/212 = 214 frames.

∴ Page Table Size = 220×14-bits ≈ 220×16-bits ≈ 220×2B = 2MB.

Virtual Address Space

The virtual address space is 32 bits, which allows for a total of 2^32 unique addresses.

Each page size is 4 KB (kilobytes), equivalent to 2^12 bytes.

Therefore, the total number of pages in the virtual address space is 2^32 / 2^12 = 2^20 pages.

Physical Address Space

The physical memory size is 64 MB (megabytes), which equals 2^26 bytes.
Each frame (physical page) corresponds to the page size of 4 KB (2^12 bytes).
Thus, the total number of frames in physical memory is 2^26 / 2^12 = 2^14 frames.

Page Table Size

To map each virtual page to a physical frame, we need an entry in the page table for each page.

Since there are 2^20 pages, the page table requires 2^20 entries.

Assuming each entry is 4 bytes (32 bits), the total size of the page table is:

Page Table Size = 2^20 * 4 bytes = 2 MB.

Therefore, the approximate size of the page table is 2 MB.

<https://www.geeksforgeeks.org/multilevel-paging-in-operating-system/>
