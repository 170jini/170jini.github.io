---
layout: post
title: Jetpack Compose - TextField / OutlinedTextField
description: Jetpack Compose - TextField / OutlinedTextField
summary: Jetpack Compose - TextField / OutlinedTextField
tags: 
minute: 1
---
TextField
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
OutlinedTextField
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