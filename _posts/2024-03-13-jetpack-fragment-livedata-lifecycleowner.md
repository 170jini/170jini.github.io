---
layout: post
title: Jetpack - Fragment LiveData / LifeCycleOwner
description: Jetpack - Fragment LiveData / LifeCycleOwner
summary: Jetpack - Fragment LiveData / LifeCycleOwner
tags: 
minute: 1
---
build.gradle
```xml
buildFeatures {
    viewBinding = true
}
```
MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding : ActivityMainBinding

    val manager = supportFragmentManager

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)

        binding.btn1.setOnClickListener {
            val transaction1 = manager.beginTransaction()
            val fragment1 = BlankFragment1()
            transaction1.replace(R.id.frameArea, fragment1)
            transaction1.addToBackStack(null)
            transaction1.commit()
        }

        binding.btn2.setOnClickListener {
            val transaction2 = manager.beginTransaction()
            val fragment2 = BlankFragment2()
            transaction2.replace(R.id.frameArea, fragment2)
            transaction2.addToBackStack(null)
            transaction2.commit()
        }
    }
}
```
BlankFragment1.kt
```kotlin
class BlankFragment1 : Fragment() {

    private val TAG = "BlankFragment1"

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        Log.d(TAG, "onCreate")
    }

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        // Inflate the layout for this fragment
        return inflater.inflate(R.layout.fragment_blank1, container, false)
    }

    override fun onDestroyView() {
        super.onDestroyView()
        Log.d(TAG, "onDestroyView")
    }

    override fun onDestroy() {
        super.onDestroy()
        Log.d(TAG, "onDestroy")
    }
}
```
BlankFragment2.kt
```kotlin
class BlankFragment2 : Fragment() {

    private val TAG = "BlankFragment2"

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        Log.d(TAG, "onCreate")
    }

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        // Inflate the layout for this fragment
        return inflater.inflate(R.layout.fragment_blank2, container, false)
    }

    override fun onDestroyView() {
        super.onDestroyView()
        Log.d(TAG, "onDestroyView")
    }

    override fun onDestroy() {
        super.onDestroy()
        Log.d(TAG, "onDestroy")
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
        android:layout_height="match_parent"
        android:orientation="vertical">

        <Button
            android:id="@+id/btn1"
            android:text="btn1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/btn2"
            android:text="btn2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <androidx.fragment.app.FragmentContainerView
            android:id="@+id/frameArea"
            android:name="com.sim.myapplication.BlankFragment1"
            android:layout_width="match_parent"
            android:layout_height="match_parent"/>

    </LinearLayout>

</androidx.constraintlayout.widget.ConstraintLayout>
```
fragment_blank1.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".BlankFragment1">

    <!-- TODO: Update blank fragment layout -->
    <TextView
        android:textSize="60sp"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:text="Frag1" />

</FrameLayout>
```
fragment_blank2.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".BlankFragment2">

    <!-- TODO: Update blank fragment layout -->
    <TextView
        android:textSize="60sp"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:text="Frag2" />

</FrameLayout>
```