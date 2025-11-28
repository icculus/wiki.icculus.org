# PHYSFS_DEPRECATED

A macro to tag a symbol as deprecated.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
#define PHYSFS_DEPRECATED __attribute__((deprecated))
```

## Remarks

A function is marked deprecated by adding this macro to its declaration:

```c
extern PHYSFS_DEPRECATED int ThisFunctionWasABadIdea(void);
```

Compilers with deprecation support can give a warning when a deprecated
function is used. This symbol may be used in PhysicsFS's headers, but apps
are welcome to use it for their own interfaces as well.

PhysicsFS, on occasion, might deprecate a function for various reasons.
However, PhysicsFS never removes symbols before major versions, at a
minimum, so deprecated interfaces in PhysicsFS 3 will remain available at
least until PhysicsFS 4, where it would be expected an app would have to
take steps to migrate anyhow.

Historically, PhysicsFS has _never_ removed a deprecated symbol, but this
is not promised forever!

On compilers without a deprecation mechanism, this is defined to nothing,
and using a deprecated function will not generate a warning.

## Version

This macro is available since PhysicsFS 2.1.0.

----
[CategoryAPI](CategoryAPI), [CategoryAPIMacro](CategoryAPIMacro), [CategoryPhysicsFS](CategoryPhysicsFS)

