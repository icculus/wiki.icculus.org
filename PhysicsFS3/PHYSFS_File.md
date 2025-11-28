# PHYSFS_File

A PhysicsFS file handle.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef struct PHYSFS_File
{
    void *opaque;  /**< That's all you get. Don't touch. */
} PHYSFS_File;
```

## Remarks

You get a pointer to one of these when you open a file for reading,
writing, or appending via PhysicsFS.

As you can see from the lack of meaningful fields, you should treat this as
opaque data. Don't try to manipulate the file handle, just pass the pointer
you got, unmolested, to various PhysicsFS APIs.

## Version

This struct is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_openRead](PHYSFS_openRead)
- [PHYSFS_openWrite](PHYSFS_openWrite)
- [PHYSFS_openAppend](PHYSFS_openAppend)
- [PHYSFS_close](PHYSFS_close)
- [PHYSFS_read](PHYSFS_read)
- [PHYSFS_write](PHYSFS_write)
- [PHYSFS_seek](PHYSFS_seek)
- [PHYSFS_tell](PHYSFS_tell)
- [PHYSFS_eof](PHYSFS_eof)
- [PHYSFS_setBuffer](PHYSFS_setBuffer)
- [PHYSFS_flush](PHYSFS_flush)

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategoryPhysicsFS](CategoryPhysicsFS)

