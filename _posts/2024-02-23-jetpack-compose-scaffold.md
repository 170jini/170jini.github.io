---
layout: post
title: Jetpack Compose - Scaffold
description: Jetpack Compose - Scaffold
summary: Jetpack Compose - Scaffold
tags: 
minute: 1
---
```kotlin
Scaffold(
    topBar = {
        TopAppBar(
            title = {
                Text(text = "Main")
            },
            navigationIcon = {
                IconButton(
                    onClick = {
                    }
                ) {
                    Icon(Icons.Default.Add, contentDescription = "add")
                }
            },
            actions = {
                Button(
                    onClick = {
                    }
                ) {
                    Text(text = "Btn")
                }
            },
            colors = topAppBarColors(
                Color.Red
            )
        )
    },
    floatingActionButton = {
        FloatingActionButton(
            onClick = {
            }
        ) {
            Icon(Icons.Default.Menu, contentDescription = "Menu")
        }
    },
    bottomBar = {
        BottomAppBar(
            containerColor = Color.Red
        ) {
            Row(
                modifier = Modifier.fillMaxSize(),
                horizontalArrangement = Arrangement.SpaceBetween
            ) {
                IconButton(
                    onClick = {
                    }
                ) {
                    Icon(Icons.Default.Home, contentDescription = "Home")
                }
                IconButton(
                    onClick = {
                    }
                ) {
                    Icon(Icons.Default.Favorite, contentDescription = "Favorite")
                }
                IconButton(
                    onClick = {
                    }
                ) {
                    Icon(Icons.Default.Settings, contentDescription = "Settings")
                }
            }
        }
    }
) {
    Surface(
        modifier = Modifier
            .fillMaxSize()
            .padding(paddingValues = it)
    ) {
        Text(text = "This is content")
    }
}
```