---
layout: post
title: Jetpack Compose - ProgressIndicator
description: Jetpack Compose - ProgressIndicator
summary: Jetpack Compose - ProgressIndicator
tags: 
minute: 1
---
```kotlin
var progress by remember { mutableStateOf(0.0f) }

Column(
    modifier = Modifier.fillMaxSize(),
    verticalArrangement = Arrangement.Center,
    horizontalAlignment = Alignment.CenterHorizontally
) {
    Button(onClick = {
        if (progress < 1.0f) {
            progress += 0.1f
        }
    }) {
        Text(
            text = "행복게이지",
            fontSize = 30.sp
        )
    }
    Spacer(modifier = Modifier.size(30.dp))
    LinearProgressIndicator(
        progress = progress,
        modifier = Modifier.height(10.dp),
        color = Color.Red,
        trackColor = Color.Cyan
    )
    Spacer(modifier = Modifier.size(30.dp))
    CircularProgressIndicator(
        progress = progress,
        color = Color.Red
    )
}
```