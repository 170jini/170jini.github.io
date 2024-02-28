---
layout: post
title: Jetpack Compose - Retrofit
description: Jetpack Compose - Retrofit
summary: Jetpack Compose - Retrofit
tags: 
minute: 1
---
AndroidMenifest.xml
```xml
<uses-permission android:name="android.permission.INTERNET"/>
```
build.gradle
```xml
implementation("com.squareup.retrofit2:retrofit:2.9.0")
implementation("com.squareup.retrofit2:converter-gson:2.9.0")
```
retrofit1
```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MyApplicationTheme {
                val coroutineScope = rememberCoroutineScope()
                val retrofitInstance = RetrofitInstance.getInstance().create(MyApi::class.java)
                Box(
                    modifier = Modifier.fillMaxSize(),
                    contentAlignment = Alignment.Center
                ) {
                    Button(
                        onClick = {
                            coroutineScope.launch {
                                val response = retrofitInstance.getPost1()
                                Log.d("MainActivity", response.body().toString())
                            }
                        }
                    ) {
                        Text(text = "CALL API")
                    }
                }
            }
        }
    }
}

data class Post(
    val userId : Int,
    val id : Int,
    val title : String,
    val body : String
)

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

interface MyApi {
    @GET("posts/1")
    suspend fun getPost1() : Response<Post>
}
```