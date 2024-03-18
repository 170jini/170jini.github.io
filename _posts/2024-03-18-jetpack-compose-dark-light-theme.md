---
layout: post
title: Jetpack Compose - Dark / Light Theme
description: Jetpack Compose - Dark / Light Theme
summary: Jetpack Compose - Dark / Light Theme
tags: 
minute: 1
---
```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MythTheme(
                darkTheme = true
            ) {
                ThemeTest1()
            }
        }
    }
}

@Composable
fun ThemeTest1() {
    Surface(
        modifier = Modifier.fillMaxSize(),
        color = MaterialTheme.colorScheme.background
    ) {
        Text(text = "HELLO")
    }
}

@Preview(
    showBackground = true,
    uiMode = Configuration.UI_MODE_NIGHT_NO,
    name = "Light"
)
@Preview(
    showBackground = true,
    uiMode = Configuration.UI_MODE_NIGHT_YES,
    name = "Dark"
)
@Composable
fun GreetingPreview() {
    MythTheme {
        ThemeTest1()
    }
}
```