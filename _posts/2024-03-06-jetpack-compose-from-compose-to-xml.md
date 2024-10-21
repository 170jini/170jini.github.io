---
layout: post
title: Jetpack Compose - Compose -> XML
description: Jetpack Compose - Compose -> XML
summary: Jetpack Compose - Compose -> XML
tags: 
minute: 1
---
MainActivity.kt
```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MyApplicationTheme {
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    Greeting("Android")
                }
            }
        }
    }
}

@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    val context = LocalContext.current
    Text(
        text = "Hello $name",
        modifier = modifier.clickable {
            val intent = Intent(context, HappyActivity::class.java)
            context.startActivity(intent)
        }
    )
}
```
activity_happy.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".HappyActivity">
    <TextView
        android:text="If you're listening to the lecture, you're the champion"
        android:textSize="50sp"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
</androidx.constraintlayout.widget.ConstraintLayout>
```
AndroidManifest.xml
```xml
<activity
    android:name=".HappyActivity"
    android:exported="false"
    android:theme="@style/Theme.AppCompat.Light"/>
```