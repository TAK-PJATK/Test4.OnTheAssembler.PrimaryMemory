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
