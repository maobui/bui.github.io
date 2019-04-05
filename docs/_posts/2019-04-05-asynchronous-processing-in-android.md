---
layout: default
title:  "The ways to do asynchronous processing in Android and counting"
date:   2019-004-05 23:44:36 +0700
categories: blog
---
**The ways to do asynchronous processing in Android and counting**


You are able to move a part of your code into another thread to offload the main thread and avoid getting ANR, NetworkOnMainThreadException, IllegalStateException(e.g. Cannot access database on the main thread since it may potentially lock the UI for a long period of time).

There are some approaches that you should choose depends on the situation

``Java Thread or Android HandlerThread``

    Java threads are one-time use only and die after executing its run method.

    HandlerThread is a handy class for starting a new thread that has a looper.

``AsyncTask``

    AsyncTask is designed to be a helper class around Thread and Handler and does not constitute a generic threading framework. AsyncTasks should ideally be used for short operations (a few seconds at the most.) If you need to keep threads running for long periods of time, it is highly recommended you use the various APIs provided by the java.util.concurrent package such as Executor, ThreadPoolExecutor and FutureTask.

``Thread pool implementation ThreadPoolExecutor, ScheduledThreadPoolExecutor...``

    ThreadPoolExecutor class that implements ExecutorService which gives fine control on the thread pool (Eg, core pool size, max pool size, keep alive time, etc.)

    ScheduledThreadPoolExecutor - a class that extends ThreadPoolExecutor. It can schedule tasks after a given delay or periodically.

``FutureTask``

    FutureTask performs asynchronous processing, however, if the result is not ready yet or processing has not complete, calling get() will be block the thread

``AsyncTaskLoaders``

    AsyncTaskLoaders as they solve a lot of problems that are inherent to AsyncTask

``IntentService``

    This is the defacto choice for long running processing on Android, a good example would be to upload or download large files. The upload and download may continue even if the user exits the app and you certainly do not want to block the user from being able to use the app while these tasks are going on.

``JobScheduler``

    Effectively, you have to create a Service and create a job using JobInfo.Builder that specifies your criteria for when to run the service.

``RxJava``

    Library for composing asynchronous and event-based programs by using observable sequences.

``Coroutines (Kotlin)``

    The main gist of it is, it makes asynchronous code looks so much like synchronous

Read more here:
[8 ways to do asynchronous processing in Android and counting](https://android.jlelse.eu/8-ways-to-do-asynchronous-processing-in-android-and-counting-f634dc6fae4e){:target="_blank"}
[The Evolution of Android Network Access](https://medium.com/@elye.project/the-evolution-of-android-network-access-1e199fc6e9a2){:target="_blank"}
[Using a Thread Pool in Android]{https://medium.com/@frank.tan/using-a-thread-pool-in-android-e3c88f59d07f){:target="_blank"}
[Managing Threads and Custom Services](https://guides.codepath.com/android/Managing-Threads-and-Custom-Services#handlerthread-caveats){:target="_blank"}

**From**
*   [stackoverflow](https://stackoverflow.com/questions/6343166/how-do-i-fix-android-os-networkonmainthreadexception#49338894){:target="_blank"}