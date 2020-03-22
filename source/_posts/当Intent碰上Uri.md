---
title: 当Intent碰上Uri
date: 2020-03-22 17:30:20
categories:
  - 网络日志
tags:
  - Android
  - Intent
  - Kotlin
---

![源自https://unsplash.com/](https://raw.githubusercontent.com/x13945/image-bucket/master/img/markus-spiske-70Rir5vB96U-unsplash.jpg)

# 问题描述

最近的工作中，涉及到在`Android`的`BroadcastReceiver`的使用，这本是`Android`开发中常见的场景。但是当我用来**隐式启动**`BroadcastReceiver`的`Intent`中通过`setData`方法携带了一个`Uri`的时候，`BroadcastReceiver`却无法被`Intent`唤醒了。

```java
/**
 * Set the data this intent is operating on.  This method automatically
 * clears any type that was previously set by {@link #setType} or
 * {@link #setTypeAndNormalize}.
 *
 * <p><em>Note: scheme matching in the Android framework is
 * case-sensitive, unlike the formal RFC. As a result,
 * you should always write your Uri with a lower case scheme,
 * or use {@link Uri#normalizeScheme} or
 * {@link #setDataAndNormalize}
 * to ensure that the scheme is converted to lower case.</em>
 *
 * @param data The Uri of the data this intent is now targeting.
 *
 * @return Returns the same Intent object, for chaining multiple calls
 * into a single statement.
 *
 * @see #getData
 * @see #setDataAndNormalize
 * @see android.net.Uri#normalizeScheme()
 */
public @NonNull Intent setData(@Nullable Uri data) {
    mData = data;
    mType = null;
    return this;
}
```

经过测试之后，发现如果`Intent`中同时设置了`Action`和`Uri`的时候，`Action`相当于是失效状态，这个不光是涉及到

`BroadcastReceiver`，连`Activity`的表现也是如此。

发现了问题，当然要解决呀，下面是经过复盘后精简出的两个可以验证失效的最小场景：

## BroadcastReceiver的隐式启动

首先，在`AndroidManifest`中注册我们的`BroadcastReceiver`及其`intent-filter`:

```xml
<receiver
    android:exported="true"
    android:name=".EmptyReceiver">
    <intent-filter>
        <action android:name="com.test.ACTION_RECEIVER"/>
    </intent-filter>
</receiver>
```
然后，在`Kotlin`中尝试用如下的代码来启动`EmptyReceiver`:

```kotlin
sendBroadcast(Intent("com.test.ACTION_RECEIVER").apply {
  data = Uri.parse("https://blog.lstec.org")
})
```

之后就会发现这个`BroadcastReceiver`并没有被启动。

## Activity的隐式启动

首先，在`AndroidManifest`中注册我们的`Activity`及其`intent-filter`:

```xml


<activity
    android:exported="true"
    android:name=".EmptyActivity">
    <intent-filter>
        <action android:name="com.test.ACTION_ACTIVITY"/>
    </intent-filter>
</activity>
```

然后，在`Kotlin`中尝试用如下的代码来启动`EmptyActivity`:

```kotlin
startActivity(Intent("com.test.ACTION_ACTIVITY").apply {
  data = Uri.parse("https://blog.lstec.org")
})
```

之后就会发现这个`EmptyActivity`并没有被启动。

# 原理探究

既然问题已经暴露，我们就要尽量查出问题产生的根本原因，而不是仅仅找个规避方案了事。经过一番代码跟踪之后，我发现这个问题在`BroadcastReceiver`和`Activity`中的表现是一致的，连原因也是同一个，那么我下面就用`BroadcastReceiver`举例，说一下这个问题的根本原因。

## 1. BroadcastReceiver的分发

众所周知，`BroadcastReceiver`的分发也是由`framework`中的`AMS`来处理的，就是它：`frameworks/base/services/core/java/com/android/server/am/ActivityManagerService.java`。经过一番调查之后，发现`AMS`收到一个`BroadcastReceiver`请求的时候，会通过它的成员变量`mReceiverResolver`来查找哪些`BroadcastReceiver`可以处理这个`Intent`。

```java

    /**
     * Resolver for broadcast intents to registered receivers.
     * Holds BroadcastFilter (subclass of IntentFilter).
     */
    final IntentResolver<BroadcastFilter, BroadcastFilter> mReceiverResolver
            = new IntentResolver<BroadcastFilter, BroadcastFilter>() {
        ......
        被忽略的其他代码
        ......
    }

```

下面我们就要分析这个`mReceiverResolver`是如何工作的。

## 2. IntentResolver查找对应的BroadcastReceiver

`AMS`通过`IntentResolver`的`queryIntent`来查找Intent对应的那些`BroadcastReceiver`。这个方法的定义大致如下：

```java
    public List<R> queryIntent(Intent intent, String resolvedType, boolean defaultOnly,
            int userId)
```

经过我的梳理，这个方法的工作流程大致如下：

```java

    public List<R> queryIntent(Intent intent, String resolvedType, boolean defaultOnly,
            int userId) {
        // Uri中的scheme，如Uri是https://google.com，那么scheme就是https
        String scheme = intent.getScheme();
        ArrayList<R> finalList = new ArrayList<R>();

        F[] firstTypeCut = null;

        // If the intent includes a MIME type, then we want to collect all of
        // the filters that match that MIME type.
        if (resolvedType != null) {
          // 由于 resolvedType 是空的，所以这里不执行
        }

        // If the intent includes a data URI, then we want to collect all of
        // the filters that match its scheme (we will further refine matches
        // on the authority and path by directly matching each resulting filter).
        if (scheme != null) {
            schemeCut = mSchemeToFilter.get(scheme);
        }

        // If the intent does not specify any data -- either a MIME type or
        // a URI -- then we will only be looking for matches against empty
        // data.
        if (resolvedType == null && scheme == null && intent.getAction() != null) {
          // 由于 scheme 不为空，所以这里不执行
            firstTypeCut = mActionToFilter.get(intent.getAction());
        }

        FastImmutableArraySet<String> categories = getFastIntentCategories(intent);
        if (firstTypeCut != null) {
          // 由于 firstTypeCut 为null，所以这里不执行
            buildResolveList(intent, categories, debug, defaultOnly, resolvedType,
                    scheme, firstTypeCut, finalList, userId);
        }

        return finalList;
    }

```

由此可见，当`Intent`中既有`Action`，又有`Uri`的时候，`Action`就会被忽略。

# 总结

当我们使用的`Intent`去隐式启动`BroadcastReceiver`或者 `Activity`，如果`Intent`里既有`Action`，又有`Uri`。我们需要在组件的`intent-filter`显式声明我们能够捕获该`Uri`的`scheme`。类似"https://m.lstec.org"的uri，需要在`AndroidManifest.xml` 中用如下的方式声明：

```xml
<intent-filter>
    <action android:name="com.test.ACTION_RECEIVER" />
    <category android:name="android.intent.category.DEFAULT" />
    <data android:scheme="wmpfos" />
</intent-filter>
```



