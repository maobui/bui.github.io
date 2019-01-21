---
layout: default
title:  "The application may be doing too much work on its main thread"
date:   2018-12-26 23:44:36 +0700
categories: blog
---
**Warning: The application may be doing too much work on its main thread
Try this sorce code:**

```java
 public void onCreate() {
     if (DEVELOPER_MODE) {
         StrictMode.setThreadPolicy(new StrictMode.ThreadPolicy.Builder()
                 .detectDiskReads()
                 .detectDiskWrites()
                 .detectNetwork()   // or .detectAll() for all detectable problems
                 .penaltyLog()
                 .build());
         StrictMode.setVmPolicy(new StrictMode.VmPolicy.Builder()
                 .detectLeakedSqlLiteObjects()
                 .detectLeakedClosableObjects()
                 .penaltyLog()
                 .penaltyDeath()
                 .build());
     }
     super.onCreate();
 }
```

**On developer android**
*   [StrictMode](https://developer.android.com/reference/android/os/StrictMode){:target="_blank"}