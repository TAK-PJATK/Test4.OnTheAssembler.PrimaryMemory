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
