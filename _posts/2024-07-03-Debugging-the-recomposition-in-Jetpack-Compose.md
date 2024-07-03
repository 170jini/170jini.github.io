---
layout: post
title: "Debugging the recomposition in Jetpack Compose"
description: "Debugging the recomposition in Jetpack Compose"
summary: "Debugging the recomposition in Jetpack Compose"
tags: 
minute: 1
---
[Reference](https://medium.com/proandroiddev/debugging-the-recomposition-in-jetpack-compose-16e92cbc9c6)    

__*State*__    
State is the pivot in the declarative world. Recomposition happens when there is a modification in the state. There are two methods for altering a state value, which will consequently trigger recomposition:    
- Update the inputs of the function.    
- Update the state variable, typically done through mutableStateOf.    
Let’s break down how state functions within a composable. Consider the following example:    
```kotlin
@Composable
private fun SimpleTextField() {
    var text = ""

    TextField(value = text, onValueChange = {
        text = it
    })
}
```
This composable won’t work because text is just a local variable and its value won’t persist during recomposition.    
So, how can we resolve this?    
```kotlin
@Composable
private fun SimpleTextField() {
    var text by remember { mutableStateOf("") }

    TextField(value = text, onValueChange = {
        text = it
    })
}
```
In this adjustment, we’ve performed two actions:    
- By assigning text with mutableStateOf(), we declare that the text is now a state, to be precise, a mutable state.    
- By inserting remember, we ensure that the value of this text is retained across recompositions.    
With these changes, the TextField should now function properly.    