# PHYSFS_getRealDir

Figure out where in the search path a file resides.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
const char * PHYSFS_getRealDir(const char *filename);
```

## Function Parameters

|              |              |                   |
| ------------ | ------------ | ----------------- |
| const char * | **filename** | file to look for. |

## Return Value

(const char *) Returns READ ONLY string of element of search path
containing the the file in question. NULL if not found.

## Remarks

The file is specified in platform-independent notation. The returned
filename will be the element of the search path where the file was found,
which may be a directory, or an archive. Even if there are multiple matches
in different parts of the search path, only the first one found is used,
just like when opening a file.

So, if you look for "maps/level1.map", and C:\\mygame is in your search
path and C:\\mygame\\maps\\level1.map exists, then "C:\mygame" is returned.

If a any part of a match is a symbolic link, and you've not explicitly
permitted symlinks, then it will be ignored, and the search for a match
will continue.

If you specify a fake directory that only exists as a mount point, it'll be
associated with the first archive mounted there, even though that directory
isn't necessarily contained in a real archive.

**WARNING**: This will return NULL if there is no real directory associated
with `filename`. Specifically, [PHYSFS_mountIo](PHYSFS_mountIo)(),
[PHYSFS_mountMemory](PHYSFS_mountMemory)(), and
[PHYSFS_mountHandle](PHYSFS_mountHandle)() will return NULL even if the
filename is found in the search path. Plan accordingly.

## Thread Safety

It is safe to call this function from any thread.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

