---
layout: post
title: Jetpack Compose - Code Editing
description: Jetpack Compose - Code Editing
summary: Jetpack Compose - Code Editing
tags: 
minute: 1
---
```kotlin
@Composable
fun MyTextArea1() {
    Column {
        Text(
            text = "안녕",
            fontSize = 100.sp,
            color = Color.Red
        )
        Text(
            text = "나는",
            fontSize = 100.sp,
            color = Color.Gray
        )
        Text(
            text = "누구야",
            fontSize = 100.sp,
            color = Color.Green
        )
    }
}

@Composable
fun MyTextArea2() {
    Column {
        MyTextFormat1(text = "안녕", fontSize = 100.sp, color = Color.Red)
        MyTextFormat1(text = "나는", fontSize = 100.sp, color = Color.Green)
        MyTextFormat1(text = "누구야", fontSize = 100.sp, color = Color.Gray)
    }
}

@Composable
fun MyTextFormat1(text : String, fontSize : TextUnit, color : Color) {
    Text(
        text = text,
        fontSize = fontSize,
        color = color
    )
}

@Composable
fun MyTextArea3() {
    MyTextFormat2 {
        Text(
            text = "안녕",
            fontSize = 100.sp,
            color = Color.Red
        )
    }
}

@Composable
fun MyTextFormat2(content : @Composable () -> Unit) {
    Column {
        content()
        content()
        content()
        content()
        content()
    }
}
```