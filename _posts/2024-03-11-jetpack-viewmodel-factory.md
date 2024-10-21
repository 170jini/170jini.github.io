---
layout: post
title: Jetpack - ViewModel Factory
description: Jetpack - ViewModel Factory
summary: Jetpack - ViewModel Factory
tags: 
minute: 1
---
MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    lateinit var viewModel: MainViewModel
    lateinit var viewModelFactory: MainViewModelFactory

    override fun onCreate(savedInstanceState: Bundle?) {

        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        viewModelFactory = MainViewModelFactory(5000)
        viewModel = ViewModelProvider(this, viewModelFactory).get(MainViewModel::class.java)
    }
}
```
MainViewModel.kt
```kotlin
class MainViewModel(num : Int) : ViewModel() {
    init {
        Log.d("MainViewModel", num.toString())
    }
}
```
MainViewModelFactory.kt
```kotlin
class MainViewModelFactory(private val num : Int) : ViewModelProvider.Factory {
    override fun <T : ViewModel> create(modelClass: Class<T>): T {
        if (modelClass.isAssignableFrom(MainViewModel::class.java)) {
            return MainViewModel(num) as T
        }
        throw IllegalArgumentException("Unknown ViewModel class")
    }
}
```