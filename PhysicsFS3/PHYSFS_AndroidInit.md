# PHYSFS_AndroidInit

Android-specific initialization details.

## Header File

Defined in [<physfs.h>](https://github.com/icculus/physfs/blob/main/src/physfs.h)

## Syntax

```c
typedef struct PHYSFS_AndroidInit
{
    void *jnienv;  /**< a valid JNIEnv * for the app. */
    void *context; /**< a valid Context * for the app. */
} PHYSFS_AndroidInit;
```

## Remarks

This data is only used on Android. Other platforms can ignore this (and the
struct will be preprocessed out too).

This struct must hold a valid JNIEnv * and a JNI object of a Context
(either the application context or the current Activity is fine). Both are
cast to a void * so we don't need jni.h included wherever physfs.h is.

This _must_ be used with [PHYSFS_init](PHYSFS_init) or various APIs, like
[PHYSFS_getBaseDir](PHYSFS_getBaseDir)() and
[PHYSFS_getPrefDir](PHYSFS_getPrefDir)(), will fail on Android.

## See Also

- [PHYSFS_init](PHYSFS_init)

----
[CategoryAPI](CategoryAPI), [CategoryAPIStruct](CategoryAPIStruct), [CategoryPhysicsFS](CategoryPhysicsFS)

