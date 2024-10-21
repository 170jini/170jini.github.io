---
layout: post
title: Jetpack Compose - Button / Toast
description: Jetpack Compose - Button / Toast
summary: Jetpack Compose  - Button / Toast
tags: 
minute: 1
---
```kotlin
val context = LocalContext.current

Button(
    onClick = {
        Log.d("tag", "msg")
        Toast.makeText(context, "click", Toast.LENGTH_LONG).show()
    },
    colors = ButtonDefaults.buttonColors(
        containerColor = Color.Yellow,
        contentColor = Color.Blue
    ),
    modifier = Modifier
        .width(200.dp)
        .height(300.dp)
) {
    Text(
        text = "Button,Button,Button,Button,Button,Button",
        lineHeight = 50.sp,
        fontSize = 30.sp,
        color = Color.Red
    )
}
```