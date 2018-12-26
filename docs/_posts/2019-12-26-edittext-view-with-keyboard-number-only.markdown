---
layout: default
title:  "Edittext view with keyboard number only"
date:   2019-12-26 23:44:36 +0700
categories: blog
---
##### [](#header-1) After several tries, I got it! I'm setting the keyboard values programmatically like that

```java
myEditText.setInputType(InputType.TYPE_CLASS_NUMBER | InputType.TYPE_NUMBER_VARIATION_PASSWORD); 
```
##### [](#header-2) Or if you want you go with the XML view is like:
```xml
android: inputType = "numberPassword"
```

##### [](#header-3) Both configs gonna display a password bullets, and as far as we are looking display numbers on the EditText we need to create a custom ClickableSpan class.

```java
 private class NumericKeyBoardTransformationMethod extends PasswordTransformationMethod {
    @Override
    public CharSequence getTransformation(CharSequence source, View view) {
        return source;
    }
}
```

##### [](#header-4) And finally we need implementing it to the EditText in order to display the characters typed.

```java
myEditText.setTransformationMethod(new NumericKeyBoardTransformationMethod());
```

##### [](#header-5) This is how my keyboard looks like now

![](https://i.stack.imgur.com/8gYx4.png)


#### [](#header-6) On stackoverflow
1.  [link1](https://stackoverflow.com/questions/13817521/edittext-view-with-keyboard-number-only/13817572){:target="_blank"}
2.  [link2](https://stackoverflow.com/questions/37525471/android-keyboard-showing-numbers){:target="_blank"}