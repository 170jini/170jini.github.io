---
layout: post
title: Jetpack Compose - Column / Spacer / Divider
description: Jetpack Compose - Column / Spacer / Divider
summary: Jetpack Compose  - Column / Spacer / Divider
tags: 
minute: 1
---
```kotlin
Column(
    modifier = Modifier.padding(30.dp)
) {
    Text(
        text = "1",
        fontSize = 30.sp
    )
    Spacer(modifier = Modifier.padding(30.dp))
    Divider(
        thickness = 4.dp,
        color = Color.Blue
    )
    Spacer(modifier = Modifier.padding(30.dp))
    Text(
        text = "2",
        fontSize = 30.sp
    )
    Text(
        text = "3",
        fontSize = 30.sp
    )
}
```