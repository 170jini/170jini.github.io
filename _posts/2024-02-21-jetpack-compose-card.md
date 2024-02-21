---
layout: post
title: Jetpack Compose - Card
description: Jetpack Compose - Card
summary: Jetpack Compose - Card
tags: 
minute: 1
---
```kotlin
@Composable
fun Greeting(txt: String) {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .height(100.dp)
            .padding(10.dp),
        elevation = CardDefaults.cardElevation(
            defaultElevation = 3.dp
        ),
        shape = RoundedCornerShape(50.dp),
        border = BorderStroke(1.dp, Color.Black)
    ) {
        Box(modifier = Modifier
            .fillMaxSize()
            .background(Color.Blue),
            contentAlignment = Alignment.Center
        ) {
            Text(
                text = txt,
                fontSize = 30.sp
            )
        }
    }
}

@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    MyApplicationTheme {
        Column() {
            Greeting("1")
            Greeting("2")
            Greeting("3")
            Greeting("4")
        }
    }
}
```