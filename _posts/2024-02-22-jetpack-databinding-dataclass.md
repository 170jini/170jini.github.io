---
layout: post
title: Jetpack - DataBinding + DataClass
description: Jetpack - DataBinding + DataClass
summary: Jetpack - DataBinding + DataClass
tags: 
minute: 1
---
build.gradle
```xml
buildFeatures {
    dataBinding = true
}
```
MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding : ActivityMainBinding

    var testCount = 20

    override fun onCreate(savedInstanceState: Bundle?) {

        super.onCreate(savedInstanceState)
        binding = DataBindingUtil.setContentView(this, R.layout.activity_main)

        val person = Person("Ryan", 20)
        binding.user = person
    }

    fun myClick(view : View) {
        Log.d("tag", "msg")
        testCount++

        val person = Person("Ryan", testCount)
        binding.user = person
    }
}
```
activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>

<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <data>
        <variable
            name="user"
            type="com.sim.myapplication.Person" />
    </data>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:textSize="100dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@{user.name}"
            />

        <TextView
            android:textSize="100dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@{Integer.toString(user.age)}"
            />

        <TextView
            android:textSize="100dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@{user.age > 30 ? `Old` : `Youg`}"
            />

        <Button
            android:text="btn"
            android:onClick="myClick"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

    </LinearLayout>

</layout>
```
Person.kt
```kotlin
data class Person(
    val name : String,
    val age : Int
)
```