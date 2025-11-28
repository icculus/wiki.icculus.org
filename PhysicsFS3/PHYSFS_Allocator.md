# PHYSFS_Allocator

PhysicsFS allocation function pointers.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef struct PHYSFS_Allocator
{
    int (*Init)(void);   /**< Initialize. Can be NULL. Zero on failure. */
    void (*Deinit)(void);  /**< Deinitialize your allocator. Can be NULL. */
    void *(*Malloc)(PHYSFS_uint64);  /**< Allocate like malloc(). */
    void *(*Realloc)(void *, PHYSFS_uint64); /**< Reallocate like realloc(). */
    void (*Free)(void *); /**< Free memory from Malloc or Realloc. */
} PHYSFS_Allocator;
```

## Remarks

(This is for limited, hardcore use. If you don't immediately see a need for
it, you can probably ignore this forever.)

You create one of these structures for use with
[PHYSFS_setAllocator](PHYSFS_setAllocator). Allocators are assumed to be
reentrant by the caller; please mutex accordingly.

Allocations are always discussed in 64-bits, for future expansion...we're
on the cusp of a 64-bit transition, and we'll probably be allocating 6
gigabytes like it's nothing sooner or later, and I don't want to change
this again at that point. If you're on a 32-bit platform and have to
downcast, it's okay to return NULL if the allocation is greater than 4
gigabytes, since you'd have to do so anyhow.

## Version

This struct is available since PhysicsFS 2.0.0.

## See Also

- [PHYSFS_setAllocator](PHYSFS_setAllocator)

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategoryPhysicsFS](CategoryPhysicsFS)

