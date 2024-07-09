---
layout: post
title: "Kotlin Tip #19: Use the APPLY Function to Configure Complex Objects— 100 Kotlin Tips in 100 Days"
description: "Kotlin Tip #19: Use the APPLY Function to Configure Complex Objects— 100 Kotlin Tips in 100 Days"
summary: "Kotlin Tip #19: Use the APPLY Function to Configure Complex Objects— 100 Kotlin Tips in 100 Days"
tags: 
minute: 1
---
[Reference](https://medium.com/kotlin-with-raphael-de-lio/kotlin-tip-19-use-the-apply-function-to-configure-complex-objects-100-kotlin-tips-in-100-days-3979b09c9e61)    

In our previous tip, we talked about how the run function can help us initialize and process objects. The apply function also serves as a mechanism for configuring objects. However, differently from the run function, it returns the context object itself.    

This feature is particularly advantageous when you’re working with an object that requires multiple initializations or configurations. Apply allows for direct access to the object’s members without needing to reference the object explicitly, making your code more concise and fluid.    

```kotlin
class DatabaseConnection {
    var host: String = ""
    var port: Int = 0
    var dbName: String = ""
    var username: String = ""
    var password: String = ""

    fun connect() {
        println("Connecting to database $dbName at $host:$port with username $username")
    }
}

fun main() {
    val dbConnection = DatabaseConnection().apply {
        host = "localhost"
        port = 5432
        dbName = "myDatabase"
        username = "admin"
        password = "password"
    }

    dbConnection.connect()
}
```

Here’s how it works: apply is called on an object and takes a lambda expression. Within this lambda, every call or access to the object’s properties or functions is implicitly made on the context object. Upon completion, apply returns the context object, now fully configured.    

Not only does this reduce the overall verbosity of your code, but it also enhances clarity. Each property is set within a block that clearly denotes its purpose: configuring the DatabaseConnection object.

