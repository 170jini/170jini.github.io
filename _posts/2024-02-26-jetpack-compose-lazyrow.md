---
layout: post
title: Jetpack Compose - LazyRow
description: Jetpack Compose - LazyRow
summary: Jetpack Compose - LazyRow
tags: 
minute: 1
---
```kotlin
val textList = listOf(
    "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q"
)

LazyRow {
    items(textList) { item ->
        Text(
            text = item,
            fontSize = 100.sp,
            modifier = Modifier.clickable {
                println("Clicked item : $item")
            }
        )
    }
}
```