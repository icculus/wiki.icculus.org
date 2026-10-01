# MOJOELF_getmmaprange

Determine the full address space of a loaded ELF binary.

## Header File

Defined in [<mojoelf.h>](https://github.com/icculus/mojoelf/blob/main/mojoelf.h)

## Syntax

```c
void MOJOELF_getmmaprange(void *lib, void **addr, unsigned long *len);
```

## Function Parameters

|                 |          |                                                         |
| --------------- | -------- | ------------------------------------------------------- |
| void *          | **lib**  | a handle from a MojoELF-opened ELF binary.              |
| void **         | **addr** | on return, contains the mmap'd base address for `lib`.  |
| unsigned long * | **len**  | on return, set to the number of bytes mmap'd for `lib`. |

## Remarks

An ELF binary is loaded to specific addresses with mmap(). This function
returns the starting address of that mapped range, and the number of bytes
mapped. This tells you the block of memory that the the ELF is occupying.

What is at a specific address in that memory block, whether it is code or
data, and what memory protections any given page has, are not guaranteed.
It is not a copy of the ELF binary, but different sections of it mapped as
specified in the original binary.

Most applications don't need to use this function.

## Thread Safety

this function is not thread-safe.

## Version

This function is available since MojoELF 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryMojoELF](CategoryMojoELF)

