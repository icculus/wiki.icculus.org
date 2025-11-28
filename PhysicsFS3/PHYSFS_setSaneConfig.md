# PHYSFS_setSaneConfig

Set up sane, default paths.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
int PHYSFS_setSaneConfig(const char *organization,
      const char *appName,
      const char *archiveExt,
      int includeCdRoms,
      int archivesFirst);
```

## Function Parameters

|              |                   |                                                                                                                                                                                                                                                                                                                                                                              |
| ------------ | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| const char * | **organization**  | Name of your company/group/etc to be used as a dirname, so keep it small, and no-frills.                                                                                                                                                                                                                                                                                     |
| const char * | **appName**       | Program-specific name of your program, to separate it from other programs using PhysicsFS.                                                                                                                                                                                                                                                                                   |
| const char * | **archiveExt**    | File extension used by your program to specify an archive. For example, Quake 3 uses "pk3", even though they are just zipfiles. Specify NULL to not dig out archives automatically. Do not specify the '.' char; If you want to look for ZIP files, specify "ZIP" and not ".ZIP" ... the archive search is case-insensitive.                                                 |
| int          | **includeCdRoms** | Non-zero to include CD-ROMs in the search path, and (if `archiveExt` != NULL) search them for archives. This may cause a significant amount of blocking while discs are accessed, and if there are no discs in the drive (or even not mounted on Unix systems), then they may not be made available anyhow. You may want to specify zero and handle the disc setup yourself. |
| int          | **archivesFirst** | Non-zero to prepend the archives to the search path. Zero to append them. Ignored if !`archiveExt`.                                                                                                                                                                                                                                                                          |

## Return Value

(int) Returns nonzero on success, zero on error. Use
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() to obtain the specific
error.

## Remarks

Helper function.

The write dir will be set to the pref dir returned by
[PHYSFS_getPrefDir](PHYSFS_getPrefDir)(organization, appName), which is
created if it doesn't exist.

The above is sufficient to make sure your program's configuration directory
is separated from other clutter, and platform-independent.

The search path will be:

- The Write Dir (created if it doesn't exist)
- The Base Dir ([PHYSFS_getBaseDir](PHYSFS_getBaseDir)())
- All found CD-ROM dirs (optionally)

These directories are then searched for files ending with the extension
`archiveExt`, which, if they are valid and supported archives, will also be
added to the search path. If you specified "PKG" for `archiveExt`, and
there's a file named data.PKG in the base dir, it'll be checked. Archives
can either be appended or prepended to the search path in alphabetical
order, regardless of which directories they were found in. All archives are
mounted in the root of the virtual file system ("/").

All of this can be accomplished from the application, but this just does it
all for you. Feel free to add more to the search path manually, too.

## Thread Safety

This function is not thread safe.

## Version

This function is available since PhysicsFS 1.0.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIFunction](CategoryAPIFunction), [CategoryPhysicsFS](CategoryPhysicsFS)

