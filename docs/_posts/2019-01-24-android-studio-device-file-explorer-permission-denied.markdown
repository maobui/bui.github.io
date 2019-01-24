---
layout: default
title:  "Android studio device file explorer permission denied"
date:   2019-01-24 23:44:36 +0700
categories: blog
---
**Android studio device file explorer permission denied**

By design `adb root` command works in development builds only (i.e. `eng` and `userdebug` which have `ro.debuggable=1` by default). So to enable the `adb root` command on your otherwise rooted device just add the `ro.debuggable=1` line to one of the following files:

```bash
    /system/build.prop
    /system/default.prop
    /data/local.prop
```

If you want `adb shell` to start as root by default - then add `ro.secure=0` as well.

Alternatively you could use modified `adbd` binary (which does not check for `ro.debuggable`)

From https://android.googlesource.com/platform/system/core/+/master/adb/daemon/main.cpp

```c++
    #if defined(ALLOW_ADBD_ROOT)
    // The properties that affect `adb root` and `adb unroot` are ro.secure and
    // ro.debuggable. In this context the names don't make the expected behavior
    // particularly obvious.
    //
    // ro.debuggable:
    //   Allowed to become root, but not necessarily the default. Set to 1 on
    //   eng and userdebug builds.
    //
    // ro.secure:
    //   Drop privileges by default. Set to 1 on userdebug and user builds.
```

**On stackoverflow**
*   [stackoverflow](https://stackoverflow.com/questions/25477424/adb-shell-su-works-but-adb-root-does-not){:target="_blank"}