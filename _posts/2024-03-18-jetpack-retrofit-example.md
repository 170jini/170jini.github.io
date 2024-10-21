---
layout: post
title: Jetpack - Retrofit 간단한 예제
description: Jetpack - Retrofit 간단한 예제
summary: Jetpack - Retrofit 간단한 예제
tags: 
minute: 1
---
AndroidManifest.xml
```xml
<uses-permission android:name="android.permission.INTERNET"/>
```
build.gradle
```xml
implementation("com.squareup.retrofit2:retrofit:2.9.0")
implementation("com.squareup.retrofit2:converter-gson:2.9.0")
```
MainActivity.kt
```kotlin
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val api = RetrofitInstance.getInstance().create(MyApi::class.java)
        api.getPost1().enqueue(object : Callback<Post> {
            override fun onResponse(call: Call<Post>, response: Response<Post>) {
                Log.d("API1", response.toString())
            }
            override fun onFailure(call: Call<Post>, t: Throwable) {
                Log.d("API1", "fail")
            }
        })
        api.getPostNumber(2).enqueue(object : Callback<Post> {
            override fun onResponse(call: Call<Post>, response: Response<Post>) {
                Log.d("API2", response.toString())
            }
            override fun onFailure(call: Call<Post>, t: Throwable) {
                Log.d("API2", "fail")
            }
        })
    }
}
```
RetrofitInstance.kt
```kotlin
object RetrofitInstance {
    val BASE_URL = "https://jsonplaceholder.typicode.com/"
    val client = Retrofit
        .Builder()
        .baseUrl(BASE_URL)
        .addConverterFactory(GsonConverterFactory.create())
        .build()
    fun getInstance() : Retrofit {
        return client
    }
}
```
Post.kt
```kotlin
data class Post(
    val userId : Int,
    val id : Int,
    val title : String,
    val body : String
)
```
MyApi.kt
```kotlin
interface MyApi {
    @GET("posts/1")
    fun getPost1() : Call<Post>
    @GET("posts/{number}")
    fun getPostNumber(
        @Path("number") number : Int
    ) : Call<Post>
}
```