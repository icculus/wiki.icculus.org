# PHYSFS_stat

Get various information about a directory or a file.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_stat(const char *fname, PHYSFS_Stat *stat);
```

## Function Parameters

|                              |           |                                                          |
| ---------------------------- | --------- | -------------------------------------------------------- |
| const char *                 | **fname** | filename to check, in platform-indepedent notation.      |
| [PHYSFS_Stat](PHYSFS_Stat) * | **stat**  | pointer to structure to fill in with data about `fname`. |

## Return Value

(int) Returns non-zero on success, zero on failure. On failure, `stat`'s
contents are undefined.

## Remarks

Obtain various information about a file or directory from the meta data.

This function will never follow symbolic links. If you haven't enabled
symlinks with [PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)(),
stat'ing a symlink will be treated like stat'ing a non-existant file. If
symlinks are enabled, stat'ing a symlink will give you information on the
link itself and not what it points to.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 2.1.0.

## See Also

- [PHYSFS_Stat](PHYSFS_Stat)

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

