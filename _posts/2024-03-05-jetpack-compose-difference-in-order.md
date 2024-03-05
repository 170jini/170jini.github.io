---
layout: post
title: Jetpack Compose - background / padding 순서에 따른 차이
description: Jetpack Compose - background / padding 순서에 따른 차이
summary: Jetpack Compose - background / padding 순서에 따른 차이
tags: 
minute: 1
---
```kotlin
@Composable
fun MyBoxTest() {
    Column {
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(200.dp)
                .background(Color.Green)
                .clip(RoundedCornerShape(30.dp))
                .padding(20.dp)
        ) {
            Text(text = "test")
        }
        Spacer(modifier = Modifier.padding(20.dp))
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(200.dp)
                .clip(RoundedCornerShape(30.dp))
                .background(Color.Green)
                .padding(20.dp)
        ) {
            Text(text = "test")
        }
        Spacer(modifier = Modifier.padding(20.dp))
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(200.dp)
                .padding(20.dp)
                .clip(RoundedCornerShape(30.dp))
                .background(Color.Green)
        ) {
            Text(text = "test")
        }
    }
}
```