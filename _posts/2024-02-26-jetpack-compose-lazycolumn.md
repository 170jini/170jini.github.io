---
layout: post
title: Jetpack Compose - LazyColumn
description: Jetpack Compose - LazyColumn
summary: Jetpack Compose - LazyColumn
tags: 
minute: 1
---
```kotlin
val textList = listOf(
    "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q",
    "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q",
    "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q",
    "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q"
)

LazyColumn {
    items(textList) { item ->
        Text(
            text = item,
            fontSize = 60.sp,
            modifier = Modifier.fillMaxWidth()
        )
    }
}
```