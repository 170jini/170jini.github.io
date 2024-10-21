---
layout: post
title: Jetpack - Fragment에서 ViewModel 사용
description: Jetpack - Fragment에서 ViewModel 사용
summary: Jetpack - Fragment에서 ViewModel 사용
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

    val manager = supportFragmentManager

    override fun onCreate(savedInstanceState: Bundle?) {

        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val transaction = manager.beginTransaction()
        val fragment = TestFragment()
        transaction.replace(R.id.frameArea, fragment)
        transaction.addToBackStack(null)
        transaction.commit()
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

    <FrameLayout
        android:id="@+id/frameArea"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</androidx.constraintlayout.widget.ConstraintLayout>
```
TestFragment.kt
```kotlin
class TestFragment : Fragment() {

    private lateinit var binding : FragmentTestBinding

    private lateinit var viewmodel : TestFragmentViewModel

    override fun onAttach(context: Context) {
        super.onAttach(context)
        Log.d("TestFragment", "onAttach")
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        Log.d("TestFragment", "onCreate")
    }

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        Log.d("TestFragment", "onCreateView")
        binding = DataBindingUtil.inflate(inflater, R.layout.fragment_test, container, false)
        viewmodel = ViewModelProvider(this).get(TestFragmentViewModel::class.java)
        binding.resultArea.text = viewmodel.getCount().toString()
        binding.plus.setOnClickListener {
            viewmodel.plus()
            binding.resultArea.text = viewmodel.getCount().toString()
        }
        binding.minus.setOnClickListener {
            viewmodel.minus()
            binding.resultArea.text = viewmodel.getCount().toString()
        }
        return binding.root
    }

    override fun onResume() {
        super.onResume()
        Log.d("TestFragment", "onResume")
    }

    override fun onStop() {
        super.onStop()
        Log.d("TestFragment", "onStop")
    }

    override fun onDestroyView() {
        super.onDestroyView()
        Log.d("TestFragment", "onDestroyView")
    }

    override fun onDestroy() {
        super.onDestroy()
        Log.d("TestFragment", "onDestroy")
    }

    override fun onDetach() {
        super.onDetach()
        Log.d("TestFragment", "onDetach")
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

        </LinearLayout>

    </FrameLayout>
</layout>
```
TestFragmentViewModel.kt
```kotlin
class TestFragmentViewModel : ViewModel() {
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