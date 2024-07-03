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
__*Recomposition*__    
Compose starts identifying the scope of changes as soon as there are updates with inputs or states. To illustrate, let’s check this example:    
```kotlin
@Composable
fun Sample() {
    var button1 by remember { mutableStateOf("button 1") }
    var button2 by remember { mutableStateOf("button 2") }

    Column(horizontalAlignment = Alignment.CenterHorizontally) {
        // Recomposes when `button1` changes, but not when button2 changes
        Button(onClick = { button1 += "1" }) { Text(text = button1) }

        Spacer(modifier = Modifier.height(8.dp))

        // Recomposes when `button2` changes, but not when button1 changes
        Button(onClick = { button2 += "2" }) { Text(text = button2) }
    }
}
```
The best way to debug how many times a composable is being recomposed is to use Layout Inspector (Android Studio > Tools > Layout inspector).    
This behaves as expected, composables recompose independently when reading updated states.    
Composition works in the following way:    
1. Initial State: The entire composable gets composed with the initial values.    
2. User clicks on button1: Its state variable updates, triggering a recomposition within the first button’s scope.    
3. User clicks on button2: Its state variable updates separately from button1, leading to recomposition within the second button’s scope.    
