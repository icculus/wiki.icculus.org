# PhysicsFS 3.0

The latest version of this library is available from [GitHub](https://github.com/icculus/physfs/releases).

PhysicsFS provides a cross-platform "Virtual File System" (VFS) API. It is intended for use in games, although it could work in other apps as well.

The app provides directories and archives in various formats, and builds an interpolated file tree of all their contents, with different
pieces mounted at different points in the tree. This makes it easy to provide game data, local files, mods, updates, etc, overriding 
pieces of the tree as appropriate.

It can also enumerate physical media (CD and DVD discs, etc), although this is less useful in modern times, and provides some helpful unicode functionality, which is definitely still useful!

It is available under the zlib license, found in the file [LICENSE.txt](https://github.com/icculus/physfs/blob/main/LICENSE.txt).

A more detailed overview, and a list of available APIs, can be viewed in [CategoryPhysicsFS](CategoryPhysicsFS).

Enjoy!

