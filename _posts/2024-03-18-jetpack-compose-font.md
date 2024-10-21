---
layout: post
title: Jetpack Compose - Font
description: Jetpack Compose - Font
summary: Jetpack Compose - Font
tags: 
minute: 1
---
```kotlin
val bmFont1 = FontFamily(Font(resId = R.font.bmjua))
val bmFont2 = FontFamily(Font(resId = R.font.bmyeonsung))

val typography = Typography(
    bodyLarge = TextStyle(
        fontFamily = bmFont1,
        fontWeight = FontWeight.Normal,
        fontSize = 50.sp,
        lineHeight = 24.sp,
        letterSpacing = 0.5.sp
    ),
    titleLarge = TextStyle(
        fontFamily = bmFont2,
        fontWeight = FontWeight.Normal,
        fontSize = 50.sp,
        lineHeight = 28.sp,
        letterSpacing = 0.sp
    )
)

@Composable
fun Test() {
    Column {
        Text(
            text = "폰트1",
            style = typography.bodyLarge // MaterialTheme.typography.bodyLarge
        )
        Text(
            text = "폰트2",
            style = typography.titleLarge // MaterialTheme.typography.titleLarge
        )
    }
}
```