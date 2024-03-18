---
layout: post
title: Jetpack - 기존 Retrofit의 CallBack Hell
description: Jetpack - 기존 Retrofit의 CallBack Hell
summary: Jetpack - 기존 Retrofit의 CallBack Hell
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
                api.getPostNumber(2).enqueue(object : Callback<Post> {
                    override fun onResponse(call: Call<Post>, response: Response<Post>) {
                        Log.d("API2", response.toString())
                        api.getPostNumber(3).enqueue(object : Callback<Post> {
                            override fun onResponse(call: Call<Post>, response: Response<Post>) {
                                Log.d("API3", response.toString())
                                api.getPostNumber(4).enqueue(object : Callback<Post> {
                                    override fun onResponse(call: Call<Post>, response: Response<Post>) {
                                        Log.d("API4", response.toString())
                                    }
                                    override fun onFailure(call: Call<Post>, t: Throwable) {
                                        Log.d("API4", "fail")
                                    }
                                })
                            }
                            override fun onFailure(call: Call<Post>, t: Throwable) {
                                Log.d("API3", "fail")
                            }
                        })
                    }
                    override fun onFailure(call: Call<Post>, t: Throwable) {
                        Log.d("API2", "fail")
                    }
                })
            }
            override fun onFailure(call: Call<Post>, t: Throwable) {
                Log.d("API1", "fail")
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