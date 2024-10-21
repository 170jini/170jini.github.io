---
layout: post
title: Jetpack - SQLite 간단한 예제
description: Jetpack - SQLite 간단한 예제
summary: Jetpack - SQLite 간단한 예제
tags: 
minute: 1
---
MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    lateinit var db : SQLiteHelperSample

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        db = SQLiteHelperSample(this)

        val inputArea = findViewById<EditText>(R.id.inputArea)
        val insertBtn = findViewById<Button>(R.id.insert)
        val getAllBtn = findViewById<Button>(R.id.getAll)
        val deleteBtn = findViewById<Button>(R.id.deleteAll)
        val resultBtn = findViewById<TextView>(R.id.resultArea)

        insertBtn.setOnClickListener {
            val inputText = inputArea.text.toString()
            db.insert(inputText)
            inputArea.setText("")
        }

        getAllBtn.setOnClickListener {
            val arr = db.getAllData()
            resultBtn.text = arr.toString()
        }

        deleteBtn.setOnClickListener {
            db.deleteAll()
        }
    }

    override fun onDestroy() {
        super.onDestroy()
        db.close()
    }
}
```
SQLiteHelperSample.kt
```kotlin
class SQLiteHelperSample(context: Context) : SQLiteOpenHelper(context, DATABASE_NAME, null, DATABASE_VERSION) {

    companion object {
        private const val DATABASE_VERSION = 1
        private const val DATABASE_NAME = "myTestDB.db"
        private const val TBL_NAME = "my_table"

        private const val ID = "id"
        private const val TITLE = "title"
    }

    override fun onCreate(db: SQLiteDatabase?) {
        val SQL_CREATE_ENTRIES =
            "CREATE TABLE $TBL_NAME (" +
                    "$ID INTEGER PRIMARY KEY," +
                    "$TITLE TEXT)"

        db?.execSQL(SQL_CREATE_ENTRIES)
    }

    fun insert(str : String) {
        val db = this.writableDatabase

        val values = ContentValues().apply {
            put(TITLE, str)
        }

        db.insert(TBL_NAME, null, values)
    }

    fun getAllData() : ArrayList<String> {
        val db = this.readableDatabase
        val query = "SELECT * FROM $TBL_NAME"

        val cursor = db.rawQuery(query, null)

        val arr = ArrayList<String>()

        with(cursor) {
            while (moveToNext()) {
                arr.add(getString(1))
            }
        }

        return arr
    }

    fun deleteAll() {
        val db = this.writableDatabase
        db.execSQL("DELETE FROM $TBL_NAME")
    }

    override fun onUpgrade(db: SQLiteDatabase?, oldVersion: Int, newVersion: Int) {
        db?.execSQL("DROP TABLE IF EXISTS $TBL_NAME")
        onCreate(db)
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

        <EditText
            android:id="@+id/inputArea"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/insert"
            android:text="insert"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/getAll"
            android:text="getAll"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/deleteAll"
            android:text="deleteAll"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <TextView
            android:text="resultArea"
            android:id="@+id/resultArea"
            android:textSize="30sp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

    </LinearLayout>

</androidx.constraintlayout.widget.ConstraintLayout>
```