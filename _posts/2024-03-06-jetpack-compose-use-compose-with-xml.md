---
layout: post
title: Jetpack Compose - Compose <-> XML 같이쓰기
description: Jetpack Compose - Compose <-> XML 같이쓰기
summary: Jetpack Compose - Compose <-> XML 같이쓰기
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
    val progressValue = remember { mutableStateOf(0) }
    Column(
        modifier = Modifier.fillMaxSize(),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        AndroidView(
            factory = { context ->
                val view = LayoutInflater.from(context).inflate(R.layout.temp_xml, null, false)
                view
            },
            update = { view ->
                val progressBar = view.findViewById<ProgressBar>(R.id.progressBar)
                progressBar.progress = progressValue.value
            },
            modifier = Modifier.fillMaxWidth()
        )
        Button(
            onClick = {
                progressValue.value += 10
            }
        ) {
            Text(text = "UP")
        }
    }
}
```
temp_xml.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <ProgressBar
        android:id="@+id/progressBar"
        style="?android:attr/progressBarStyleHorizontal"
        android:layout_width="200dp"
        android:layout_height="wrap_content"
        android:max="100"
        android:progress="50"
        android:secondaryProgress="75"
        android:layout_gravity="center"/>
</LinearLayout>
```