---
layout: post
title: Jetpack Compose - Show / Hide
description: Jetpack Compose - Show / Hide
summary: Jetpack Compose - Show / Hide
tags: 
minute: 1
---
```kotlin
@Composable
fun MyShowHideEx1() {
    var isButtonVisible by remember { mutableStateOf(false) }

    Column(
        modifier = Modifier.fillMaxSize(),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Button(
            onClick = {
                isButtonVisible = !isButtonVisible
                println(isButtonVisible)
            }
        ) {
            if(isButtonVisible) {
                Text(
                    text = "숨기기",
                    fontSize = 50.sp
                )
            } else {
                Text(
                    text = "보이기",
                    fontSize = 50.sp
                )
            }
        }
        if(isButtonVisible) {
            Button(onClick = { /*TODO*/ }) {
                Text(
                    text = "짠짠짠",
                    fontSize = 50.sp
                )
            }
        }
    }
}

@Composable
fun MyShowHideEx2() {
    var switchState by remember {
        mutableStateOf(false)
    }
    Column(
        modifier = Modifier.padding(20.dp)
    ) {
        Switch(
            checked = switchState,
            onCheckedChange = {checked ->
                switchState = checked
            }
        )
        Text(
            text = if (switchState) "ON" else "OFF",
            fontSize = 100.sp
        )
        if(switchState) {
            Button(onClick = { /*TODO*/ }) {
                Text(
                    text = "얍얍",
                    fontSize = 100.sp
                )
            }
        }
    }
}
```