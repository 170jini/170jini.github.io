---
layout: post
title: Jetpack - ROOM 간단한 예제
description: Jetpack - ROOM 간단한 예제
summary: Jetpack - ROOM 간단한 예제
tags: 
minute: 1
---
build.gradle.kts
```xml
plugins {
    id("kotlin-kapt")
}
dependencies {
    implementation("androidx.room:room-runtime:2.6.1")
    annotationProcessor("androidx.room:room-compiler:2.6.1")
    kapt("androidx.room:room-compiler:2.6.1")
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.1")
    implementation("androidx.lifecycle:lifecycle-viewmodel-ktx:2.7.0")
}
```
```kotlin
```
```kotlin
```
WordEntity.kt
```kotlin
@Entity(tableName = "word_table")
data class WordEntity(
    @PrimaryKey(autoGenerate = true)
    @ColumnInfo(name = "id")
    var id : Int,
    @ColumnInfo(name = "text")
    var text : String
)
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
        android:layout_height="match_parent"
        android:orientation="vertical">

        <EditText
            android:id="@+id/textInputArea"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/insert"
            android:text="insert"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/getData"
            android:text="getData"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/delete"
            android:text="delete"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <androidx.recyclerview.widget.RecyclerView
            android:id="@+id/rv"
            android:layout_width="match_parent"
            android:layout_height="match_parent"/>

    </LinearLayout>

</androidx.constraintlayout.widget.ConstraintLayout>
```
text_row_item.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="100dp">

    <TextView
        android:id="@+id/textView"
        android:text="text"
        android:textSize="50sp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

</LinearLayout>
```