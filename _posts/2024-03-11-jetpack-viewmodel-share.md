---
layout: post
title: Jetpack - Activity / Fragment의 ViewModel 공유
description: Jetpack - Activity / Fragment의 ViewModel 공유
summary: Jetpack - Activity / Fragment의 ViewModel 공유
tags: 
minute: 1
---
build.gradle
```xml
buildFeatures {
    dataBinding = true
}
dependencies {
    implementation("androidx.fragment:fragment-ktx:1.6.2")
}
```
MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    lateinit var binding : ActivityMainBinding
    lateinit var viewModel : MainViewModel

    override fun onCreate(savedInstanceState: Bundle?) {

        super.onCreate(savedInstanceState)

        binding = DataBindingUtil.setContentView(this, R.layout.activity_main)
        viewModel = ViewModelProvider(this).get(MainViewModel::class.java)

        binding.resultArea.text = viewModel.getCount().toString()

        binding.plus.setOnClickListener {
            viewModel.plus()
            binding.resultArea.text = viewModel.getCount().toString()
        }

        binding.minus.setOnClickListener {
            viewModel.minus()
            binding.resultArea.text = viewModel.getCount().toString()
        }

        val manager = supportFragmentManager

        binding.showFragment.setOnClickListener {
            val transaction = manager.beginTransaction()
            val fragment = TestFragment()
            transaction.replace(R.id.frameArea, fragment)
            transaction.addToBackStack(null)
            transaction.commit()
        }
    }
}
```
activity_main.xml
```xml
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical"
            android:gravity="center">

            <TextView
                android:id="@+id/resultArea"
                android:text="0"
                android:textSize="50sp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <Button
                android:id="@+id/plus"
                android:text="plus"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <Button
                android:id="@+id/minus"
                android:text="minus"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <Button
                android:id="@+id/showFragment"
                android:text="showFragment"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <FrameLayout
                android:id="@+id/frameArea"
                android:background="#32a852"
                android:layout_width="match_parent"
                android:layout_height="200dp" />

        </LinearLayout>

    </androidx.constraintlayout.widget.ConstraintLayout>

</layout>
```
TestFragment.kt
```kotlin
class TestFragment : Fragment() {

    private lateinit var binding : FragmentTestBinding
    private val viewModel : MainViewModel by activityViewModels()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
    }

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        Log.d("TestFragment", "onCreateView")
        binding = DataBindingUtil.inflate(inflater, R.layout.fragment_test, container, false)
        binding.fragmentTest.text = viewModel.getCount().toString()
        return binding.root
    }
}
```
fragment_test.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<layout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <FrameLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".TestFragment">

        <!-- TODO: Update blank fragment layout -->
        <TextView
            android:id="@+id/fragmentTest"
            android:textSize="50sp"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:text="@string/hello_blank_fragment"/>

    </FrameLayout>
</layout>
```
MainViewModel.kt
```kotlin
class MainViewModel : ViewModel() {
    var countValue = 0
    fun plus() {
        countValue++
    }
    fun minus() {
        countValue--
    }
    fun getCount() : Int {
        return countValue
    }
}
```