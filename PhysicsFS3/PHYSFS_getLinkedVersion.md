# PHYSFS_getLinkedVersion

Get the version of PhysicsFS that is linked against your program.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
void PHYSFS_getLinkedVersion(PHYSFS_Version *ver);
```

## Function Parameters

|                                    |         |                                                         |
| ---------------------------------- | ------- | ------------------------------------------------------- |
| [PHYSFS_Version](PHYSFS_Version) * | **ver** | the [PHYSFS_Version](PHYSFS_Version) struct to fill in. |

## Remarks

If you are using a shared library (DLL) version of PhysFS, then it is
possible that it will be different than the version you compiled against.

This is a real function; the macro [PHYSFS_VERSION](PHYSFS_VERSION) tells
you what version of PhysFS you compiled against:

```c
PHYSFS_Version compiled;
PHYSFS_Version linked;

PHYSFS_VERSION(&compiled);
PHYSFS_getLinkedVersion(&linked);
printf("We compiled against PhysFS version %d.%d.%d ...\n",
          compiled.major, compiled.minor, compiled.patch);
printf("But we linked against PhysFS version %d.%d.%d.\n",
          linked.major, linked.minor, linked.patch);
```

This function may be called safely at any time, even before
[PHYSFS_init](PHYSFS_init)().

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

## See Also

- [PHYSFS_VERSION](PHYSFS_VERSION)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

