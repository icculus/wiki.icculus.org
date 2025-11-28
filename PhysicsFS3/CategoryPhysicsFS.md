# CategoryPhysicsFS

The latest version of PhysicsFS can be found at:

https://icculus.org/physfs/

PhysicsFS; a portable, flexible file i/o abstraction.

This API gives you access to a system file system in ways superior to the
stdio or system i/o calls. The brief benefits:

- It's portable.
- It's safe. No file access is permitted outside the specified dirs.
- It's flexible. Archives (.ZIP files) can be used transparently as
  directory structures.

With PhysicsFS, you have a single writing directory and multiple
directories (the "search path") for reading. You can think of this as a
filesystem within a filesystem. If (on Windows) you were to set the writing
directory to "C:\MyGame\MyWritingDirectory", then no PHYSFS calls could
touch anything above this directory, including the "C:\MyGame" and "C:\"
directories. This prevents an application's internal scripting language
from piddling over c:\\config.sys, for example. If you'd rather give PHYSFS
full access to the system's REAL file system, set the writing dir to "C:\",
but that's generally A Bad Thing for several reasons.

Drive letters are hidden in PhysicsFS once you set up your initial paths.
The search path creates a single, hierarchical directory structure. Not
only does this lend itself well to general abstraction with archives, it
also gives better support to operating systems like MacOS and Unix.
Generally speaking, you shouldn't ever hardcode a drive letter; not only
does this hurt portability to non-Microsoft OSes, but it limits your win32
users to a single drive, too. Use the PhysicsFS abstraction functions and
allow user-defined configuration options, too. When opening a file, you
specify it like it was on a Unix filesystem: if you want to write to
"C:\MyGame\MyConfigFiles\game.cfg", then you might set the write dir to
"C:\MyGame" and then open "MyConfigFiles/game.cfg". This gives an
abstraction across all platforms. Specifying a file in this way is termed
"platform-independent notation" in this documentation. Specifying a a
filename in a form such as "C:\mydir\myfile" or "MacOS hard drive:My
Directory:My File" is termed "platform-dependent notation". The only time
you use platform-dependent notation is when setting up your write directory
and search path; after that, all file access into those directories are
done with platform-independent notation.

All files opened for writing are opened in relation to the write directory,
which is the root of the writable filesystem. When opening a file for
reading, PhysicsFS goes through the search path. This is NOT the same thing
as the PATH environment variable. An application using PhysicsFS specifies
directories to be searched which may be actual directories, or archive
files that contain files and subdirectories of their own. See the end of
these docs for currently supported archive formats.

Once the search path is defined, you may open files for reading. If you've
got the following search path defined (to use a win32 example again):

- C:\\mygame
- C:\\mygame\\myuserfiles
- D:\\mygamescdromdatafiles
- C:\\mygame\\installeddatafiles.zip

Then a call to [PHYSFS_openRead](PHYSFS_openRead)("textfiles/myfile.txt")
(note the directory separator, lack of drive letter, and lack of dir
separator at the start of the string; this is platform-independent
notation) will check for C:\\mygame\\textfiles\\myfile.txt, then
C:\\mygame\\myuserfiles\\textfiles\\myfile.txt, then
D:\\mygamescdromdatafiles\\textfiles\\myfile.txt, then, finally, for
textfiles\\myfile.txt inside of C:\\mygame\\installeddatafiles.zip.
Remember that most archive types and platform filesystems store their
filenames in a case-sensitive manner, so you should be careful to specify
it correctly.

Files opened through PhysicsFS may NOT contain "." or ".." or ":" as dir
elements. Not only are these meaningless on MacOS Classic and/or Unix, they
are a security hole. Also, symbolic links (which can be found in some
archive types and directly in the filesystem on Unix platforms) are NOT
followed until you call
[PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)(). That's left to
your own discretion, as following a symlink can allow for access outside
the write dir and search paths. For portability, there is no mechanism for
creating new symlinks in PhysicsFS.

The write dir is not included in the search path unless you specifically
add it. While you CAN change the write dir as many times as you like, you
should probably set it once and stick to it. Remember that your program
will not have permission to write in every directory on Unix and NT
systems.

All files are opened in binary mode; there is no endline conversion for
textfiles. Other than that, PhysicsFS has some convenience functions for
platform-independence. There is a function to tell you the current
platform's dir separator ("\\" on windows, "/" on Unix, ":" on MacOS),
which is needed only to set up your search/write paths. There is a function
to tell you what CD-ROM drives contain accessible discs, and a function to
recommend a good search path, etc.

A recommended order for the search path is the write dir, then the base
dir, then the cdrom dir, then any archives discovered. Quake 3 does
something like this, but moves the archives to the start of the search
path. Build Engine games, like Duke Nukem 3D and Blood, place the archives
last, and use the base dir for both searching and writing. There is a
helper function ([PHYSFS_setSaneConfig](PHYSFS_setSaneConfig)()) that puts
together a basic configuration for you, based on a few parameters. Also see
the comments on [PHYSFS_getBaseDir](PHYSFS_getBaseDir)(), and
[PHYSFS_getPrefDir](PHYSFS_getPrefDir)() for info on what those are and how
they can help you determine an optimal search path.

PhysicsFS 2.0 adds the concept of "mounting" archives to arbitrary points
in the search path. If a zipfile contains "maps/level.map" and you mount
that archive at "mods/mymod", then you would have to open
"mods/mymod/maps/level.map" to access the file, even though "mods/mymod"
isn't actually specified in the .zip file. Unlike the Unix mentality of
mounting a filesystem, "mods/mymod" doesn't actually have to exist when
mounting the zipfile. It's a "virtual" directory. The mounting mechanism
allows the developer to seperate archives in the tree and avoid trampling
over files when added new archives, such as including mod support in a
game...keeping external content on a tight leash in this manner can be of
utmost importance to some applications.

PhysicsFS is mostly thread safe. The errors returned by
[PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)() are unique by thread,
and library-state-setting functions are mutex'd. For efficiency, individual
file accesses are not locked, so you can not safely
read/write/seek/close/etc the same file from two threads at the same time.
Other race conditions are bugs that should be reported/patched.

While you CAN use stdio/syscall file access in a program that has PHYSFS_*
calls, doing so is not recommended, and you can not directly use system
filehandles with PhysicsFS and vice versa (but as of PhysicsFS 2.1, you can
wrap them in a [PHYSFS_Io](PHYSFS_Io) interface yourself if you wanted to).

Note that archives need not be named as such: if you have a ZIP file and
rename it with a .PKG extension, the file will still be recognized as a ZIP
archive by PhysicsFS; the file's contents are used to determine its type
where possible.

Currently supported archive types:

- .ZIP (pkZip/WinZip/Info-ZIP compatible)
- .7Z (7zip archives)
- .ISO (ISO9660 files, CD-ROM images)
- .GRP (Build Engine groupfile archives)
- .PAK (Quake I/II archive format)
- .HOG (Descent I/II/III HOG file archives)
- .MVL (Descent II movielib archives)
- .WAD (DOOM engine archives)
- .BIN (Chasm: The Rift engine archives)
- .VDF (Gothic I/II engine archives)
- .SLB (Independence War archives)

String policy for PhysicsFS 2.0 and later:

PhysicsFS 1.0 could only deal with null-terminated ASCII strings. All high
ASCII chars resulted in undefined behaviour, and there was no Unicode
support at all. PhysicsFS 2.0 supports Unicode without breaking binary
compatibility with the 1.0 API by using UTF-8 encoding of all strings
passed in and out of the library.

All strings passed through PhysicsFS are in null-terminated UTF-8 format.
This means that if all you care about is English (ASCII characters <= 127)
then you just use regular C strings. If you care about Unicode (and you
should!) then you need to figure out what your platform wants, needs, and
offers. If you are on Windows before Win2000 and build with Unicode
support, your TCHAR strings are two bytes per character (this is called
"UCS-2 encoding"). Any modern Windows uses UTF-16, which is two bytes per
character for most characters, but some characters are four. You should
convert them to UTF-8 before handing them to PhysicsFS with
[PHYSFS_utf8FromUtf16](PHYSFS_utf8FromUtf16)(), which handles both UTF-16
and UCS-2. If you're using Unix or Mac OS X, your wchar_t strings are four
bytes per character ("UCS-4 encoding", sometimes called "UTF-32"). Use
[PHYSFS_utf8FromUcs4](PHYSFS_utf8FromUcs4)(). Mac OS X can give you UTF-8
directly from a CFString or NSString, and many Unixes generally give you C
strings in UTF-8 format everywhere. If you have a single-byte high ASCII
charset, like so-many European "codepages" you may be out of luck. We'll
convert from "Latin1" to UTF-8 only, and never back to Latin1. If you're
above ASCII 127, all bets are off: move to Unicode or use your platform's
facilities. Passing a C string with high-ASCII data that isn't UTF-8
encoded will NOT do what you expect!

Naturally, there's also [PHYSFS_utf8ToUcs2](PHYSFS_utf8ToUcs2)(),
[PHYSFS_utf8ToUtf16](PHYSFS_utf8ToUtf16)(), and
[PHYSFS_utf8ToUcs4](PHYSFS_utf8ToUcs4)() to get data back into a format you
like. Behind the scenes, PhysicsFS will use Unicode where possible: the
UTF-8 strings on Windows will be converted and used with the multibyte
Windows APIs, for example.

PhysicsFS offers basic encoding conversion support, but not a whole string
library. Get your stuff into whatever format you can work with.

Most platforms supported by PhysicsFS 2.1 and later fully support Unicode.
Some older platforms have been dropped (Windows 95, Mac OS 9). Some, like
OS/2, might be able to convert to a local codepage or will just fail to
open/create the file. Modern OSes (macOS, Linux, Windows, etc) should all
be fine.

Many game-specific archivers are seriously unprepared for Unicode (the
Descent HOG/MVL and Build Engine GRP archivers, for example, only offer a
DOS 8.3 filename, for example). Nothing can be done for these, but they
tend to be legacy formats for existing content that was all ASCII (and
thus, valid UTF-8) anyhow. Other formats, like .ZIP, don't explicitly offer
Unicode support, but unofficially expect filenames to be UTF-8 encoded, and
thus Just Work. Most everything does the right thing without bothering you,
but it's good to be aware of these nuances in case they don't.

Other stuff:

Please see the file LICENSE.txt in the source's root directory for
licensing and redistribution rights.

Please see the file CREDITS.txt in the source's "docs" directory for a more
or less complete list of who's responsible for this.

<!-- END CATEGORY DOCUMENTATION -->

## Functions

<!-- DO NOT HAND-EDIT CATEGORY LISTS, THEY ARE AUTOGENERATED AND WILL BE OVERWRITTEN, BASED ON TAGS IN INDIVIDUAL PAGE FOOTERS. EDIT THOSE INSTEAD. -->
<!-- BEGIN CATEGORY LIST: CategoryPhysicsFS, CategoryAPIFunction -->
- [PHYSFS_caseFold](PHYSFS_caseFold)
- [PHYSFS_close](PHYSFS_close)
- [PHYSFS_deinit](PHYSFS_deinit)
- [PHYSFS_delete](PHYSFS_delete)
- [PHYSFS_deregisterArchiver](PHYSFS_deregisterArchiver)
- [PHYSFS_enumerate](PHYSFS_enumerate)
- [PHYSFS_enumerateFiles](PHYSFS_enumerateFiles)
- [PHYSFS_eof](PHYSFS_eof)
- [PHYSFS_exists](PHYSFS_exists)
- [PHYSFS_fileLength](PHYSFS_fileLength)
- [PHYSFS_flush](PHYSFS_flush)
- [PHYSFS_freeList](PHYSFS_freeList)
- [PHYSFS_getAllocator](PHYSFS_getAllocator)
- [PHYSFS_getBaseDir](PHYSFS_getBaseDir)
- [PHYSFS_getCdRomDirs](PHYSFS_getCdRomDirs)
- [PHYSFS_getCdRomDirsCallback](PHYSFS_getCdRomDirsCallback)
- [PHYSFS_getDirSeparator](PHYSFS_getDirSeparator)
- [PHYSFS_getErrorByCode](PHYSFS_getErrorByCode)
- [PHYSFS_getLastError](PHYSFS_getLastError)
- [PHYSFS_getLastErrorCode](PHYSFS_getLastErrorCode)
- [PHYSFS_getLinkedVersion](PHYSFS_getLinkedVersion)
- [PHYSFS_getMountPoint](PHYSFS_getMountPoint)
- [PHYSFS_getPrefDir](PHYSFS_getPrefDir)
- [PHYSFS_getRealDir](PHYSFS_getRealDir)
- [PHYSFS_getSearchPath](PHYSFS_getSearchPath)
- [PHYSFS_getSearchPathCallback](PHYSFS_getSearchPathCallback)
- [PHYSFS_getWriteDir](PHYSFS_getWriteDir)
- [PHYSFS_init](PHYSFS_init)
- [PHYSFS_isInit](PHYSFS_isInit)
- [PHYSFS_mkdir](PHYSFS_mkdir)
- [PHYSFS_mount](PHYSFS_mount)
- [PHYSFS_mountHandle](PHYSFS_mountHandle)
- [PHYSFS_mountIo](PHYSFS_mountIo)
- [PHYSFS_mountMemory](PHYSFS_mountMemory)
- [PHYSFS_openAppend](PHYSFS_openAppend)
- [PHYSFS_openRead](PHYSFS_openRead)
- [PHYSFS_openWrite](PHYSFS_openWrite)
- [PHYSFS_permitSymbolicLinks](PHYSFS_permitSymbolicLinks)
- [PHYSFS_readBytes](PHYSFS_readBytes)
- [PHYSFS_readSBE16](PHYSFS_readSBE16)
- [PHYSFS_readSBE32](PHYSFS_readSBE32)
- [PHYSFS_readSBE64](PHYSFS_readSBE64)
- [PHYSFS_readSLE16](PHYSFS_readSLE16)
- [PHYSFS_readSLE32](PHYSFS_readSLE32)
- [PHYSFS_readSLE64](PHYSFS_readSLE64)
- [PHYSFS_readUBE16](PHYSFS_readUBE16)
- [PHYSFS_readUBE32](PHYSFS_readUBE32)
- [PHYSFS_readUBE64](PHYSFS_readUBE64)
- [PHYSFS_readULE16](PHYSFS_readULE16)
- [PHYSFS_readULE32](PHYSFS_readULE32)
- [PHYSFS_readULE64](PHYSFS_readULE64)
- [PHYSFS_registerArchiver](PHYSFS_registerArchiver)
- [PHYSFS_seek](PHYSFS_seek)
- [PHYSFS_setAllocator](PHYSFS_setAllocator)
- [PHYSFS_setBuffer](PHYSFS_setBuffer)
- [PHYSFS_setErrorCode](PHYSFS_setErrorCode)
- [PHYSFS_setRoot](PHYSFS_setRoot)
- [PHYSFS_setSaneConfig](PHYSFS_setSaneConfig)
- [PHYSFS_setWriteDir](PHYSFS_setWriteDir)
- [PHYSFS_stat](PHYSFS_stat)
- [PHYSFS_supportedArchiveTypes](PHYSFS_supportedArchiveTypes)
- [PHYSFS_swapSBE16](PHYSFS_swapSBE16)
- [PHYSFS_swapSBE32](PHYSFS_swapSBE32)
- [PHYSFS_swapSBE64](PHYSFS_swapSBE64)
- [PHYSFS_swapSLE16](PHYSFS_swapSLE16)
- [PHYSFS_swapSLE32](PHYSFS_swapSLE32)
- [PHYSFS_swapSLE64](PHYSFS_swapSLE64)
- [PHYSFS_swapUBE16](PHYSFS_swapUBE16)
- [PHYSFS_swapUBE32](PHYSFS_swapUBE32)
- [PHYSFS_swapUBE64](PHYSFS_swapUBE64)
- [PHYSFS_swapULE16](PHYSFS_swapULE16)
- [PHYSFS_swapULE32](PHYSFS_swapULE32)
- [PHYSFS_swapULE64](PHYSFS_swapULE64)
- [PHYSFS_symbolicLinksPermitted](PHYSFS_symbolicLinksPermitted)
- [PHYSFS_tell](PHYSFS_tell)
- [PHYSFS_ucs4stricmp](PHYSFS_ucs4stricmp)
- [PHYSFS_unmount](PHYSFS_unmount)
- [PHYSFS_utf16stricmp](PHYSFS_utf16stricmp)
- [PHYSFS_utf8FromLatin1](PHYSFS_utf8FromLatin1)
- [PHYSFS_utf8FromUcs2](PHYSFS_utf8FromUcs2)
- [PHYSFS_utf8FromUcs4](PHYSFS_utf8FromUcs4)
- [PHYSFS_utf8FromUtf16](PHYSFS_utf8FromUtf16)
- [PHYSFS_utf8stricmp](PHYSFS_utf8stricmp)
- [PHYSFS_utf8ToUcs2](PHYSFS_utf8ToUcs2)
- [PHYSFS_utf8ToUcs4](PHYSFS_utf8ToUcs4)
- [PHYSFS_utf8ToUtf16](PHYSFS_utf8ToUtf16)
- [PHYSFS_writeBytes](PHYSFS_writeBytes)
- [PHYSFS_writeSBE16](PHYSFS_writeSBE16)
- [PHYSFS_writeSBE32](PHYSFS_writeSBE32)
- [PHYSFS_writeSBE64](PHYSFS_writeSBE64)
- [PHYSFS_writeSLE16](PHYSFS_writeSLE16)
- [PHYSFS_writeSLE32](PHYSFS_writeSLE32)
- [PHYSFS_writeSLE64](PHYSFS_writeSLE64)
- [PHYSFS_writeUBE16](PHYSFS_writeUBE16)
- [PHYSFS_writeUBE32](PHYSFS_writeUBE32)
- [PHYSFS_writeUBE64](PHYSFS_writeUBE64)
- [PHYSFS_writeULE16](PHYSFS_writeULE16)
- [PHYSFS_writeULE32](PHYSFS_writeULE32)
- [PHYSFS_writeULE64](PHYSFS_writeULE64)
<!-- END CATEGORY LIST -->

## Datatypes

<!-- DO NOT HAND-EDIT CATEGORY LISTS, THEY ARE AUTOGENERATED AND WILL BE OVERWRITTEN, BASED ON TAGS IN INDIVIDUAL PAGE FOOTERS. EDIT THOSE INSTEAD. -->
<!-- BEGIN CATEGORY LIST: CategoryPhysicsFS, CategoryAPIDatatype -->
- [PHYSFS_EnumerateCallback](PHYSFS_EnumerateCallback)
- [PHYSFS_EnumFilesCallback](PHYSFS_EnumFilesCallback)
- [PHYSFS_sint16](PHYSFS_sint16)
- [PHYSFS_sint32](PHYSFS_sint32)
- [PHYSFS_sint64](PHYSFS_sint64)
- [PHYSFS_sint8](PHYSFS_sint8)
- [PHYSFS_StringCallback](PHYSFS_StringCallback)
- [PHYSFS_uint16](PHYSFS_uint16)
- [PHYSFS_uint32](PHYSFS_uint32)
- [PHYSFS_uint64](PHYSFS_uint64)
- [PHYSFS_uint8](PHYSFS_uint8)
<!-- END CATEGORY LIST -->

## Structs

<!-- DO NOT HAND-EDIT CATEGORY LISTS, THEY ARE AUTOGENERATED AND WILL BE OVERWRITTEN, BASED ON TAGS IN INDIVIDUAL PAGE FOOTERS. EDIT THOSE INSTEAD. -->
<!-- BEGIN CATEGORY LIST: CategoryPhysicsFS, CategoryAPIStruct -->
- [PHYSFS_Allocator](PHYSFS_Allocator)
- [PHYSFS_AndroidInit](PHYSFS_AndroidInit)
- [PHYSFS_ArchiveInfo](PHYSFS_ArchiveInfo)
- [PHYSFS_Archiver](PHYSFS_Archiver)
- [PHYSFS_File](PHYSFS_File)
- [PHYSFS_Io](PHYSFS_Io)
- [PHYSFS_Stat](PHYSFS_Stat)
- [PHYSFS_Version](PHYSFS_Version)
<!-- END CATEGORY LIST -->

## Enums

<!-- DO NOT HAND-EDIT CATEGORY LISTS, THEY ARE AUTOGENERATED AND WILL BE OVERWRITTEN, BASED ON TAGS IN INDIVIDUAL PAGE FOOTERS. EDIT THOSE INSTEAD. -->
<!-- BEGIN CATEGORY LIST: CategoryPhysicsFS, CategoryAPIEnum -->
- [PHYSFS_EnumerateCallbackResult](PHYSFS_EnumerateCallbackResult)
- [PHYSFS_ErrorCode](PHYSFS_ErrorCode)
- [PHYSFS_FileType](PHYSFS_FileType)
<!-- END CATEGORY LIST -->

## Macros

<!-- DO NOT HAND-EDIT CATEGORY LISTS, THEY ARE AUTOGENERATED AND WILL BE OVERWRITTEN, BASED ON TAGS IN INDIVIDUAL PAGE FOOTERS. EDIT THOSE INSTEAD. -->
<!-- BEGIN CATEGORY LIST: CategoryPhysicsFS, CategoryAPIMacro -->
- [PHYSFS_CALL](PHYSFS_CALL)
- [PHYSFS_DEPRECATED](PHYSFS_DEPRECATED)
- [PHYSFS_file](PHYSFS_file)
- [PHYSFS_VER_MAJOR](PHYSFS_VER_MAJOR)
- [PHYSFS_VER_MINOR](PHYSFS_VER_MINOR)
- [PHYSFS_VER_PATCH](PHYSFS_VER_PATCH)
- [PHYSFS_VERSION](PHYSFS_VERSION)
<!-- END CATEGORY LIST -->

----
[CategoryAPICategory](CategoryAPICategory)

