---
layout: post
title: Jetpack Compose - Image
description: Jetpack Compose - Image
summary: Jetpack Compose - Image
tags: 
minute: 1
---
```kotlin
Image(
    painter = painterResource(id = R.drawable.pexels_photo_20179666),
    contentDescription = "Tanzania Wild Sky",
    modifier = Modifier.fillMaxSize()
)
```
    
AndroidMenifest.xml
<uses-permission android:name="android.permission.INTERNET"/>

build.gradle
implementation("io.coil-kt:coil-compose:2.4.0")

```kotlin
AsyncImage(
    model = "https://images.pexels.com/photos/20179666/pexels-photo-20179666.jpeg",
    contentDescription = "Tanzania Wild Sky",
    modifier = Modifier.fillMaxSize()
)
```