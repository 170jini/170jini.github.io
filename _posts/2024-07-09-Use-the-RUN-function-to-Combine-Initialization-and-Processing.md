---
layout: post
title: "Kotlin Tip #18: Use the RUN function to Combine Initialization and Processing — 100 Kotlin Tips in 100 Days"
description: "Kotlin Tip #18: Use the RUN function to Combine Initialization and Processing — 100 Kotlin Tips in 100 Days"
summary: "Kotlin Tip #18: Use the RUN function to Combine Initialization and Processing — 100 Kotlin Tips in 100 Days"
tags: 
minute: 1
---
[Reference](https://medium.com/kotlin-with-raphael-de-lio/kotlin-tip-18-use-the-run-function-to-combine-initialization-and-processing-100-kotlin-tips-in-059c3f3eb9be)    

In our ongoing series, we’ve been unpacking the utility of Kotlin’s scope functions, and today we turn our focus to a particularly versatile member of this family: the run function. Run is a particularly useful tool for those moments when you’re looking to execute a block of operations within the context of an object.    

Consider you’re initializing a variable where you also want to execute a set of operations immediately afterward. Here’s where run shines, allowing you to encapsulate both needs into one elegant expression:    

```kotlin
class DatabaseConfiguration() {
    var host: String? = null
    var port: String? = null
    
    fun isValid() = host == null || port == null 
    
    fun connect() = DatabaseConnection(host, port)
}

class DatabaseConnection(val host: String?, val port: String?) {
    fun runQuery(query: String) = println("Running query: $query")
}

fun main() {
    val databaseConfiguration = DatabaseConfiguration()
    val connection = databaseConfiguration.run {
        // Initialization or configuration
        host = "localhost"
        port = "5739"
        
        // Execution of a block of code
        if (isValid()) error("Invalid Database Configuration")
        connect()
    }
    
    connection.runQuery("SELECT * FROM table")
}
```

Run acts upon an object (the receiver), enveloping a lambda expression. Within this lambda, direct access to the object’s members is granted, bypassing the need for explicit naming. Yet, run’s charm doesn’t end here; it returns the outcome of the lambda, marrying the benefits of context-aware operations with functional output.    

Run excels in scenarios that demand a combination of initialization/configuration and the execution of a block that produces a result. Its use promotes not just code conciseness but also the clarity and expressiveness that Kotlin advocates.