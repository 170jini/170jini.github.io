---
layout: post
title: Jetpack Compose - Dialog
description: Jetpack Compose - Dialog
summary: Jetpack Compose - Dialog
tags: 
minute: 1
---
```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun MyDialog() {
    var dialogFlag by remember {
        mutableStateOf(false)
    }
    var inputText by remember {
        mutableStateOf("")
    }
    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Button(onClick = { dialogFlag = true }) {
            Text(text = "Come Out Dialog")
        }
        if (dialogFlag) {
            AlertDialog(
                onDismissRequest = { },
                title = { Text(text = "Dialog Title")},
                text = {
                       TextField(
                           value = inputText,
                           onValueChange = { inputText = it }
                       )
                },
                confirmButton = {
                    Button(
                        onClick = { dialogFlag = false },
                        colors = ButtonDefaults.buttonColors(
                            containerColor = Color.Blue
                        )
                    ) {
                        Text(text = "OK")
                    }
                },
                dismissButton = {
                    Button(
                        onClick = { dialogFlag = false },
                        colors = ButtonDefaults.buttonColors(
                            containerColor = Color.Red
                        )
                    ) {
                        Text(text = "NO")
                    }
                }
            )
        }
        if (inputText.isNotEmpty()) {
            Text(
                text = "Text entered : $inputText",
                fontSize = 40.sp,
                lineHeight = 40.sp
            )
        }
    }
}
```