---
layout: post
title: Jetpack - ViewModel / LiveData / LifeCycleOwner
description: Jetpack - ViewModel / LiveData / LifeCycleOwner
summary: Jetpack - ViewModel / LiveData / LifeCycleOwner
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

    private lateinit var binding: ActivityMainBinding
    private lateinit var viewModel: MainViewModel

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = DataBindingUtil.setContentView(this, R.layout.activity_main)
        viewModel = ViewModelProvider(this).get(MainViewModel::class.java)
        binding.vm = viewModel
        binding.lifecycleOwner = this
        binding.next.setOnClickListener {
            viewModel.getNextData()
        }
    }
}
```
MainViewModel.kt
```kotlin
class MainViewModel : ViewModel() {
    private var _mutableWord = MutableLiveData("")
    val liveWord : LiveData<String>
        get() = _mutableWord
    private var _randomMutableWord = MutableLiveData("")
    val randomLiveWord : LiveData<String>
        get() = _randomMutableWord
    val newData = liveWord.switchMap {
        getRandomWordShuffled(it)
    }
    init {
        getNextData()
    }
    fun getNextData() {
        val currentWord = testDataList.random()
        val randomWord = currentWord.toCharArray()
        randomWord.shuffle()
        _mutableWord.value = currentWord
        _randomMutableWord.value = String(randomWord)
    }
    fun getRandomWordShuffled(word : String) : MutableLiveData<String> {
        val liveData = MutableLiveData("")
        val randomTextWord = word.toCharArray()
        randomTextWord.shuffle()
        liveData.value = String(randomTextWord)
        return liveData
    }
}
```
TestData.kt
```kotlin
val testDataList : List<String> = listOf(
    "apple",
    "strawberry",
    "pineapple",
    "peach",
    "graph",
    "melon",
    "mango"
)
```
activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>

<layout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <data>
        <variable
            name="vm"
            type="com.sim.myapplication.MainViewModel" />
    </data>

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical">

            <TextView
                android:text="@{vm.liveWord}"
                android:textSize="50sp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <TextView
                android:text="@{vm.randomLiveWord}"
                android:textSize="50sp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <TextView
                android:text="@{vm.newData}"
                android:textSize="50sp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <Button
                android:id="@+id/next"
                android:text="next"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

        </LinearLayout>

    </androidx.constraintlayout.widget.ConstraintLayout>

</layout>
```