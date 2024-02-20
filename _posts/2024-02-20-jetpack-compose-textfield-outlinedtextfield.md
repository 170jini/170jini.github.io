---
layout: post
title: Jetpack Compose - TextField / OutlinedTextField
description: Jetpack Compose - TextField / OutlinedTextField
summary: Jetpack Compose - TextField / OutlinedTextField
tags: 
minute: 1
---
```kotlin
var textState by remember { mutableStateOf("") }

TextField(
    value = textState,
    onValueChange = {
        textState = it
    },
    label = {
        Text(text = "input")
    }
)
```

```kotlin
var textState by remember { mutableStateOf("") }

OutlinedTextField(
    value = textState,
    onValueChange = {
        textState = it
    },
    label = {
        Text(text = "input")
    }
)
```