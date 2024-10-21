---
layout: post
title: Jetpack - ViewModel과 LiveData 함께 써보기
description: Jetpack - ViewModel과 LiveData 함께 써보기
summary: Jetpack - ViewModel과 LiveData 함께 써보기
tags: 
minute: 1
---
MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var viewModel : MainViewModel

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        viewModel = ViewModelProvider(this).get(MainViewModel::class.java)

        findViewById<Button>(R.id.btnArea).setOnClickListener {
            viewModel.plusLiveDataValue()
        }
        viewModel.testMutableLiveData.observe(this, Observer {
            findViewById<TextView>(R.id.textArea).text = viewModel.testMutableLiveData.value.toString()
        })
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

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <TextView
            android:id="@+id/textArea"
            android:textSize="60dp"
            android:text="0"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/btnArea"
            android:text="btn"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

    </LinearLayout>

</androidx.constraintlayout.widget.ConstraintLayout>
```
MainViewModel.kt
```kotlin
class MainViewModel : ViewModel() {
    var testMutableLiveData = MutableLiveData(0)
    fun plusLiveDataValue() {
        testMutableLiveData.value = testMutableLiveData.value!!.plus(1)
    }
}
```