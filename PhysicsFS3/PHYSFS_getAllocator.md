# PHYSFS_getAllocator

Discover the current allocator.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
const PHYSFS_Allocator * PHYSFS_getAllocator(void);
```

## Return Value

(const [PHYSFS_Allocator](PHYSFS_Allocator) *) Returns Current allocator,
as set by [PHYSFS_setAllocator](PHYSFS_setAllocator)(), or PhysicsFS's
internal, default allocator if no application defined allocator is
currently set. Will return NULL if the library is not initialized.

## Remarks

(This is for limited, hardcore use. If you don't immediately see a need for
it, you can probably ignore this forever.)

This function exposes the function pointers that make up the currently used
allocator. This can be useful for apps that want to access PhysicsFS's
internal, default allocation routines, as well as for external code that
wants to share the same allocator, even if the application specified their
own.

This call is only valid between [PHYSFS_init](PHYSFS_init)() and
[PHYSFS_deinit](PHYSFS_deinit)() calls; it will return NULL if the library
isn't initialized. As we can't guarantee the state of the internal
allocators unless the library is initialized, you shouldn't use any
allocator returned here after a call to [PHYSFS_deinit](PHYSFS_deinit)().

Do not call the returned allocator's Init() or Deinit() methods under any
circumstances.

If you aren't immediately sure what to do with this function, you can
safely ignore it altogether.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_Allocator](PHYSFS_Allocator)
- [PHYSFS_setAllocator](PHYSFS_setAllocator)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

