# PHYSFS_setAllocator

Hook your own allocation routines into PhysicsFS.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_setAllocator(const PHYSFS_Allocator *allocator);
```

## Function Parameters

|                                              |               |                                                     |
| -------------------------------------------- | ------------- | --------------------------------------------------- |
| const [PHYSFS_Allocator](PHYSFS_Allocator) * | **allocator** | Structure containing your allocator's entry points. |

## Return Value

(int) Returns zero on failure, non-zero on success. This call only fails
when used between [PHYSFS_init](PHYSFS_init)() and
[PHYSFS_deinit](PHYSFS_deinit)() calls.

## Remarks

(This is for limited, hardcore use. If you don't immediately see a need for
it, you can probably ignore this forever.)

By default, PhysicsFS will use whatever is reasonable for a platform to
manage dynamic memory (usually ANSI C malloc/realloc/free, but some
platforms might use something else), but in some uncommon cases, the app
might want more control over the library's memory management. This lets you
redirect PhysicsFS to use your own allocation routines instead. You can
only call this function before [PHYSFS_init](PHYSFS_init)(); if the library
is initialized, it'll reject your efforts to change the allocator
mid-stream. You may call this function after
[PHYSFS_deinit](PHYSFS_deinit)() if you are willing to shut down the
library and restart it with a new allocator; this is a safe and supported
operation. The allocator remains intact between deinit/init calls. If you
want to return to the platform's default allocator, pass a NULL in here.

If you aren't immediately sure what to do with this function, you can
safely ignore it altogether.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

