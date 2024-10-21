---
layout: post
title: Jetpack Compose - WebView
description: Jetpack Compose - WebView
summary: Jetpack Compose - WebView
tags: 
minute: 1
---
```kotlin
AndroidView(factory = {
    WebView(it).apply {
        loadUrl("https://www.youtube.com")
    }
})
```