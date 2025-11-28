# PHYSFS_getSearchPath

Get the current search path.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
char ** PHYSFS_getSearchPath(void);
```

## Return Value

(char **) Returns Null-terminated array of null-terminated strings. NULL if
there was a problem (read: OUT OF MEMORY).

## Remarks

The default search path is an empty list.

The returned value is an array of strings, with a NULL entry to signify the
end of the list:

```c
for (char **i = PHYSFS_getSearchPath(); *i != NULL; i++) {
    printf("[%s] is in the search path.\n", *i);
}
```

When you are done with the returned information, you may dispose of the
resources by calling [PHYSFS_freeList](PHYSFS_freeList)() with the returned
pointer.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_getSearchPathCallback](PHYSFS_getSearchPathCallback)
- [PHYSFS_addToSearchPath](PHYSFS_addToSearchPath)
- [PHYSFS_removeFromSearchPath](PHYSFS_removeFromSearchPath)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

