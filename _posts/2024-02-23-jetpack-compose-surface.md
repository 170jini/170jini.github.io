---
layout: post
title: Jetpack Compose - Surface
description: Jetpack Compose - Surface
summary: Jetpack Compose - Surface
tags: 
minute: 1
---
Surface
```kotlin
Surface(
    modifier = Modifier
        .fillMaxWidth()
        .padding(10.dp),
    color = Color.Red,
    shape = RoundedCornerShape(20.dp),
    shadowElevation = 20.dp
) {
    Button(
        onClick = { },
        colors = ButtonDefaults.outlinedButtonColors(
            contentColor = Color.Green
        )
    ) {
        Text(text = "클릭해보세요")
    }
}
```
Surface
```kotlin
Surface(
    modifier = Modifier.fillMaxSize(),
    color = Color.LightGray,
    border = BorderStroke(2.dp, Color.Red),
    contentColor = Color.Blue
) {
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(20.dp),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Surface(
            modifier = Modifier
                .size(200.dp),
            color = Color.Red
        ) {
            Text(
                text = "This is Jetpack compose"
            )
        }
        Spacer(modifier = Modifier.height(20.dp))
        Text(
            text = "This is Jetpack compose Ex"
        )
    }
}
```