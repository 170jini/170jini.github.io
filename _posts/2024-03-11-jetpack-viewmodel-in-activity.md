---
layout: post
title: Jetpack - Activity에서 ViewModel 사용
description: Jetpack - Activity에서 ViewModel 사용
summary: Jetpack - Activity에서 ViewModel 사용
tags: 
minute: 1
---
MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

//    private var countValue = 0

    lateinit var viewModel: MainViewModel

    override fun onCreate(savedInstanceState: Bundle?) {

        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        viewModel = ViewModelProvider(this).get(MainViewModel::class.java)

        Log.d("MainActivity", "onCreate")

        val plusBtn : Button = findViewById(R.id.plus)
        val minusBtn : Button = findViewById(R.id.minus)

        val resultArea : TextView = findViewById(R.id.result)

        plusBtn.setOnClickListener {
            viewModel.plus()
            resultArea.text = viewModel.getCount().toString()
//            countValue++
//            resultArea.text = countValue.toString()
        }

        minusBtn.setOnClickListener {
            viewModel.minus()
            resultArea.text = viewModel.getCount().toString()
//            countValue--
//            resultArea.text = countValue.toString()
        }
    }

    override fun onStart() {
        super.onStart()

        Log.d("MainActivity", "onStart")
    }

    override fun onResume() {
        super.onResume()

        Log.d("MainActivity", "onResume")
    }

    override fun onPause() {
        super.onPause()

        Log.d("MainActivity", "onPause")
    }

    override fun onStop() {
        super.onStop()

        Log.d("MainActivity", "onStop")
    }

    override fun onDestroy() {
        super.onDestroy()

        Log.d("MainActivity", "onDestroy")
    }
}
```
MainViewModel.kt
```kotlin
class MainViewModel : ViewModel() {
    var countValue = 0
    init {
        Log.d("MainViewModel", "init")
    }
    fun plus() {
        countValue++
        Log.d("MainViewModel", countValue.toString())
    }
    fun minus() {
        countValue--
        Log.d("MainViewModel", countValue.toString())
    }
    fun getCount() : Int {
        return countValue
    }
}
```