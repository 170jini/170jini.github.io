---
layout: post
title: Jetpack Compose - Shape
description: Jetpack Compose - Shape
summary: Jetpack Compose - Shape
tags: 
minute: 1
---
```kotlin
@Composable
fun RadiusTest1() {
    Column {
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(100.dp)
                .padding(20.dp)
                .clip(MaterialTheme.shapes.extraLarge)
                .background(Color.Red)
        )
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(100.dp)
                .padding(20.dp)
                .clip(MaterialTheme.shapes.large)
                .background(Color.Red)
        )
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(100.dp)
                .padding(20.dp)
                .clip(MaterialTheme.shapes.medium)
                .background(Color.Red)
        )
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(100.dp)
                .padding(20.dp)
                .clip(MaterialTheme.shapes.small)
                .background(Color.Red)
        )
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(100.dp)
                .padding(20.dp)
                .clip(MaterialTheme.shapes.extraSmall)
                .background(Color.Red)
        )
    }
}

@Composable
fun RadiusTest2() {
    Column {
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(100.dp)
                .padding(20.dp)
                .clip(MaterialTheme.shapes.extraLarge)
                .background(Color.Blue)
        )
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(100.dp)
                .padding(20.dp)
                .clip(MaterialTheme.shapes.large)
                .background(Color.Blue)
        )
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(100.dp)
                .padding(20.dp)
                .clip(MaterialTheme.shapes.medium)
                .background(Color.Blue)
        )
    }
}
```