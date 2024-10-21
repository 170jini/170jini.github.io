---
layout: post
title: Jetpack Compose - Box
description: Jetpack Compose - Box
summary: Jetpack Compose  - Box
tags: 
minute: 1
---
```kotlin
Box(
    modifier = Modifier
        .fillMaxSize()
        .background(color = Color.Red)
) {
    Box(
        modifier = Modifier
            .size(100.dp)
            .background(color = Color.Blue)
            .padding(16.dp)
            .align(Alignment.TopStart)
    ) {
        Text(text = "TopStart")
    }
    Box(
        modifier = Modifier
            .size(100.dp)
            .background(color = Color.Green)
            .padding(16.dp)
            .align(Alignment.TopCenter)
    ) {
        Text(text = "TopCenter")
    }
    Box(
        modifier = Modifier
            .size(100.dp)
            .background(color = Color.Gray)
            .padding(16.dp)
            .align(Alignment.TopEnd)
    ) {
        Text(text = "TopEnd")
    }
    Box(
        modifier = Modifier
            .size(100.dp)
            .background(color = Color.Blue)
            .padding(16.dp)
            .align(Alignment.CenterStart)
    ) {
        Text(text = "CenterStart")
    }
    Box(
        modifier = Modifier
            .size(100.dp)
            .background(color = Color.Green)
            .padding(16.dp)
            .align(Alignment.Center)
    ) {
        Text(text = "Center")
    }
    Box(
        modifier = Modifier
            .size(100.dp)
            .background(color = Color.Gray)
            .padding(16.dp)
            .align(Alignment.CenterEnd)
    ) {
        Text(text = "CenterEnd")
    }
    Box(
        modifier = Modifier
            .size(100.dp)
            .background(color = Color.Blue)
            .padding(16.dp)
            .align(Alignment.BottomStart)
    ) {
        Text(text = "BottomStart")
    }
    Box(
        modifier = Modifier
            .size(100.dp)
            .background(color = Color.Green)
            .padding(16.dp)
            .align(Alignment.BottomCenter)
    ) {
        Text(text = "BottomCenter")
    }
    Box(
        modifier = Modifier
            .size(100.dp)
            .background(color = Color.Gray)
            .padding(16.dp)
            .align(Alignment.BottomEnd)
    ) {
        Text(text = "BottomEnd")
    }
}
```