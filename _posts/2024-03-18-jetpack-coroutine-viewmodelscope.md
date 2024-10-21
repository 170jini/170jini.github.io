---
layout: post
title: Jetpack - 간단한 코루틴(Coroutine) + ViewModelScope
description: Jetpack - 간단한 코루틴(Coroutine) + ViewModelScope
summary: Jetpack - 간단한 코루틴(Coroutine) + ViewModelScope
tags: 
minute: 1
---
build.gradle
```xml
implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.1")
implementation("androidx.lifecycle:lifecycle-viewmodel-ktx:2.7.0")
```
MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val goToSecond = findViewById<Button>(R.id.goToSecond)
        goToSecond.setOnClickListener {
            val intent = Intent(this, SecondActivity::class.java)
            startActivity(intent)
        }

        Log.d("TEST", "START")
        CoroutineScope(Dispatchers.IO).launch {
            Log.d("TEST", "CoroutineScope START")
            a()
            b()
            Log.d("TEST", "CoroutineScope END")
        }
        Log.d("TEST", "END")
    }
    suspend fun a() {
        delay(1000)
        Log.d("TEST", "AP1")
        delay(1000)
        Log.d("TEST", "AP2")
    }
    suspend fun b() {
        delay(1000)
        Log.d("TEST", "BP1")
        delay(1000)
        Log.d("TEST", "BP2")
    }
}
```
SecondActivity.kt
```kotlin
class SecondActivity : AppCompatActivity() {
    lateinit var viewModel : SecondViewModel
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_second)
        viewModel = ViewModelProvider(this).get(SecondViewModel::class.java)
        viewModel.a()
        viewModel.b()
    }
}
```
SecondViewModel.kt
```kotlin
class SecondViewModel : ViewModel() {
    fun a() {
        CoroutineScope(Dispatchers.IO).launch {
            for (i in 0..10) {
                delay(1000)
                Log.d("SecondViewModel A : ", i.toString())
            }
        }
    }
    fun b() {
        viewModelScope.launch {
            for (i in 0..10) {
                delay(1000)
                Log.d("SecondViewModel B : ", i.toString())
            }
        }
    }
}
```
activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>

<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/goToSecond"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"/>

</androidx.constraintlayout.widget.ConstraintLayout>
```
activity_second.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".SecondActivity">

</androidx.constraintlayout.widget.ConstraintLayout>
```