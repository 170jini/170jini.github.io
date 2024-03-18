---
layout: post
title: Jetpack Compose - TextStyle
description: Jetpack Compose - TextStyle
summary: Jetpack Compose - TextStyle
tags: 
minute: 1
---
```kotlin
@Composable
fun Test1() {
    Column {
        Text(
            text = "여기는 제목",
            fontSize = 30.sp,
            fontWeight = FontWeight.ExtraBold,
            modifier = Modifier.padding(30.dp)
        )
        Text(
            text = "여기는 내용",
            fontSize = 20.sp,
            fontWeight = FontWeight.Bold,
            modifier = Modifier.padding(30.dp)
        )
        Text(
            text = "여기는 하단글",
            fontSize = 10.sp,
            fontWeight = FontWeight.SemiBold,
            modifier = Modifier.padding(30.dp)
        )

        Text(
            text = "여기는 제목",
            style = MaterialTheme.typography.titleLarge,
            modifier = Modifier.padding(30.dp)
        )
        Text(
            text = "여기는 내용",
            style = MaterialTheme.typography.titleMedium,
            modifier = Modifier.padding(30.dp)
        )
        Text(
            text = "여기는 하단글",
            style = MaterialTheme.typography.titleSmall,
            modifier = Modifier.padding(30.dp)
        )
    }
}

@Composable
fun Test2() {
    Column {
        Text(
            text = "Display Large",
            style = MaterialTheme.typography.displayLarge
        )
        Text(
            text = "Display Medium",
            style = MaterialTheme.typography.displayMedium
        )
        Text(
            text = "Display Small",
            style = MaterialTheme.typography.displaySmall
        )
        Text(
            text = "Headline Large",
            style = MaterialTheme.typography.headlineLarge
        )
        Text(
            text = "Headline Medium",
            style = MaterialTheme.typography.headlineMedium
        )
        Text(
            text = "Headline Small",
            style = MaterialTheme.typography.headlineSmall
        )
        Text(
            text = "Title Large",
            style = MaterialTheme.typography.titleLarge
        )
        Text(
            text = "Title Medium",
            style = MaterialTheme.typography.titleMedium
        )
        Text(
            text = "Title Small",
            style = MaterialTheme.typography.titleSmall
        )
        Text(
            text = "Body Large",
            style = MaterialTheme.typography.bodyLarge
        )
        Text(
            text = "Body Medium",
            style = MaterialTheme.typography.bodyMedium
        )
        Text(
            text = "Body Small",
            style = MaterialTheme.typography.bodySmall
        )
        Text(
            text = "Label Large",
            style = MaterialTheme.typography.labelLarge
        )
        Text(
            text = "Label Medium",
            style = MaterialTheme.typography.labelMedium
        )
        Text(
            text = "Label Small",
            style = MaterialTheme.typography.labelSmall
        )
    }
}
```