---
layout: post
title: Jetpack Compose - Canvas
description: Jetpack Compose - Canvas
summary: Jetpack Compose - Canvas
tags: 
minute: 1
---
```kotlin
@Composable
fun MyCanvas() {
    Box(
        modifier = Modifier
            .fillMaxSize()
            .height(500.dp)
            .background(Color.Red)
    ) {
        Canvas(
            modifier = Modifier.size(200.dp).align(Alignment.Center)
        ) {
            drawCircle(Color.Black, radius = size.minDimension / 2)
        }
    }
//    Box(
//        modifier = Modifier
//            .width(100.dp)
//            .height(200.dp)
//            .background(Color.Green)
//    ) {
//        Canvas(
//            modifier = Modifier.fillMaxSize()
//        ) {
//            drawCircle(Color.Black, radius = size.minDimension / 2)
//        }
//    }
//    Box(
//        modifier = Modifier
//            .size(50.dp)
//            .background(Color.Green)
//    ) {
//        Canvas(
//            modifier = Modifier.fillMaxSize()
//        ) {
//            drawCircle(Color.Black, radius = size.minDimension / 10)
//        }
//    }
}
```