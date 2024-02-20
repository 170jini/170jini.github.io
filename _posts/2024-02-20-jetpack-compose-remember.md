---
layout: post
title: Jetpack Compose - Remember
description: Jetpack Compose - Remember
summary: Jetpack Compose  - Remember
tags: 
minute: 1
---
```kotlin
var count by remember { mutableStateOf(0) }

Button(onClick = {
    count++
},
    modifier = Modifier.fillMaxSize()
) {
    Text(
        text = "Count : $count",
        fontSize = 50.sp
    )
}
```