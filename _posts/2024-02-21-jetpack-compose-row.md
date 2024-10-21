---
layout: post
title: Jetpack Compose - Row
description: Jetpack Compose - Row
summary: Jetpack Compose - Row
tags: 
minute: 1
---
```kotlin
Row(
    modifier = Modifier.fillMaxSize().background(Color.Gray),
    horizontalArrangement = Arrangement.SpaceEvenly,
    verticalAlignment = Alignment.CenterVertically
) {
    Text(
        text = "Item1",
        style = TextStyle(background = Color.Blue),
        fontSize = 30.sp
    )
    Text(
        text = "Item2",
        style = TextStyle(background = Color.Red),
        fontSize = 30.sp
    )
    Text(
        text = "Item3",
        style = TextStyle(background = Color.Green),
        fontSize = 30.sp
    )
}
```