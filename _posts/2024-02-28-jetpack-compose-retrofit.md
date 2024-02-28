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
retrofit2
```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MyApplicationTheme {
                InsertInputData()
            }
        }
    }

    @OptIn(ExperimentalMaterial3Api::class)
    @Composable
    fun InsertInputData() {
        var inputNumber by remember {
            mutableStateOf("")
        }
        var post by remember {
            mutableStateOf<Post?>(null)
        }
        val coroutineScope = rememberCoroutineScope()
        Column(
            modifier = Modifier.fillMaxSize(),
            verticalArrangement = Arrangement.Center,
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            TextField(
                value = inputNumber,
                onValueChange = { inputNumber = it },
                label = { Text(text = "Input Number")}
            )
            Button(
                onClick = {
                    val number = inputNumber.toIntOrNull()
                    if (number != null) {
                        coroutineScope.launch {
                            post = getPostData(number)
                        }
                    }
                }
            ) {
                Text(text = "Get Data")
            }
            post?.let {
                Text(text = "UserId : " + it.userId)
                Text(text = "ID : " + it.id)
                Text(text = "Title : " + it.title)
                Text(text = "Body : " + it.body)
            }
        }
    }
    private suspend fun getPostData(number : Int) : Post? {
        val retrofitInstance = RetrofitInstance.getInstance().create(MyApi::class.java)
        val response = retrofitInstance.getPostNumber(number)
        return if (response.isSuccessful) response.body() else null
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
    @GET("posts/{number}")
    suspend fun getPostNumber(
        @Path("number") number : Int
    ) : Response<Post>
}
```