---
layout: default
title:  "ViewPager with bottom dots"
date:   2019-03-11 23:44:36 +0700
categories: blog
---
**ViewPager with bottom dots**

**No need for that much code.**

You can do all this stuff without coding so much by using only `viewpager` with `tablayout`.

**Your main Layout:**

```Xml
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <android.support.v4.view.ViewPager
        android:id="@+id/pager"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

    </android.support.v4.view.ViewPager>
    <android.support.design.widget.TabLayout
        android:id="@+id/tabDots"
        android:layout_alignParentBottom="true"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:tabBackground="@drawable/tab_selector"
        app:tabGravity="center"
        app:tabIndicatorHeight="0dp"/>
 </RelativeLayout>
 ```

Hook up your UI elements in activity or fragment as follows:

**Java Code:**

```Java
mImageViewPager = (ViewPager) findViewById(R.id.pager);
TabLayout tabLayout = (TabLayout) findViewById(R.id.tabDots);
tabLayout.setupWithViewPager(mImageViewPager, true);
```

That's it, you are good to go.

You will need to create the following xml resource file in the drawable folder.

**tab_indicator_selected.xml**

```Xml
<?xml version="1.0" encoding="utf-8"?>
<shape
    android:innerRadius="0dp"
    android:shape="ring"
    android:thickness="4dp"
    android:useLevel="false"
    xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="@color/colorAccent"/>
</shape>
```

**tab_indicator_default.xml**

```Xml
<?xml version="1.0" encoding="utf-8"?>
    <shape xmlns:android="http://schemas.android.com/apk/res/android"
            android:innerRadius="0dp"
            android:shape="ring"
            android:thickness="2dp"
            android:useLevel="false">
            <solid android:color="@android:color/darker_gray"/>
    </shape>
```

**tab_selector.xml**

```Xml
 <?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">

    <item android:drawable="@drawable/tab_indicator_selected"
          android:state_selected="true"/>

    <item android:drawable="@drawable/tab_indicator_default"/>
</selector>
```

**From**
*   [stackoverflow](https://stackoverflow.com/questions/20586619/android-viewpager-with-bottom-dots#40047719){:target="_blank"}