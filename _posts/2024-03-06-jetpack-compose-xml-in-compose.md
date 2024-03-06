---
layout: post
title: Jetpack Compose - Compose안에 XML 넣기
description: Jetpack Compose - Compose안에 XML 넣기
summary: Jetpack Compose - Compose안에 XML 넣기
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
    Column {
        Text(text = "Here Compose1", fontSize = 30.sp)
        AndroidView(factory = {context ->
            val view = LayoutInflater.from(context).inflate(R.layout.temp_xml, null, false)
            view.findViewById<TextView>(R.id.tempText).setOnClickListener {
                Toast.makeText(context, "Here Toast", Toast.LENGTH_LONG).show()
            }
            view
        })
        Text(text = "Here Compose2", fontSize = 30.sp)
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
    <TextView
        android:id="@+id/tempText"
        android:text="Here XML"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="40sp"/>
</LinearLayout>
```