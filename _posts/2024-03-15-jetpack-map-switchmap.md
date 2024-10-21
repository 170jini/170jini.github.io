---
layout: post
title: Jetpack - Map / SwitchMap
description: Jetpack - Map / SwitchMap
summary: Jetpack - Map / SwitchMap
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
        viewModel.liveCount.observe(this, Observer {
//            binding.resultArea1.text = (it + it).toString()
//            binding.resultArea2.text = (it * it).toString()
        })
        viewModel.mapLiveData.observe(this, Observer {
            binding.resultArea1.text = it.toString()
        })
        viewModel.switchMapLiveData.observe(this, Observer {
            binding.resultArea2.text = it.toString()
        })
        binding.btnArea.setOnClickListener {
            val count = if (binding.inputArea.text.isDigitsOnly()) binding.inputArea.text.toString().toInt() else 0
            viewModel.setLiveDataValue(count)
        }
    }
}
```
MainViewModel.kt
```kotlin
class MainViewModel : ViewModel() {
    private var _mutableCount = MutableLiveData(0)
    val liveCount : LiveData<Int>
        get() = _mutableCount
    val mapLiveData = liveCount.map {
        it + it
    }
    val switchMapLiveData = liveCount.switchMap {
        changeValue(it)
    }
    fun setLiveDataValue(count : Int) {
        _mutableCount.value = count
    }
    fun changeValue(count: Int) : MutableLiveData<Int> {
        val testLiveData = MutableLiveData(count * count)
        return testLiveData
    }
}
```
activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>

<layout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical">

            <EditText
                android:id="@+id/inputArea"
                android:hint="0"
                android:textSize="50sp"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"/>

            <Button
                android:id="@+id/btnArea"
                android:text="btn"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <TextView
                android:id="@+id/resultArea1"
                android:text="0"
                android:textSize="50sp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <TextView
                android:id="@+id/resultArea2"
                android:text="0"
                android:textSize="50sp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

        </LinearLayout>

    </androidx.constraintlayout.widget.ConstraintLayout>

</layout>
```