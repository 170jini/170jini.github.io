---
layout: post
title: "Kotlin Tip #15: Use Objects to Create Singletons— 100 Kotlin Tips in 100 Days"
description: "Kotlin Tip #15: Use Objects to Create Singletons— 100 Kotlin Tips in 100 Days"
summary: "Kotlin Tip #15: Use Objects to Create Singletons— 100 Kotlin Tips in 100 Days"
tags: 
minute: 1
---
[Reference](https://medium.com/kotlin-with-raphael-de-lio/kotlin-tip-15-100-kotlin-tips-in-100-days-dc1bbaf11d67)    

Typically, whenever you initialize a class, you’re creating a new object. In other words, each time you use the new keyword or call a constructor in Kotlin, a distinct instance of that class is allocated in memory.    

Sometimes, you don’t want a class to be able to be instantiated multiple times. Instead, you need a guarantee that only one instance of the class exists throughout the application’s lifecycle. This requirement is common in scenarios where a shared resource or a central point of control is necessary — for example, managing a connection to a database, or holding application-wide configuration settings.    

In Java, the simplest way to implement a singleton pattern is to make use of a private constructor and a static method that returns the instance of the singleton class. Take a look:    
```kotlin
public class MySingleton {
    // Private static variable of the same class that is the only instance of the class
    private static MySingleton instance;

    // Private constructor to prevent instantiation from other classes
    private MySingleton() {}

    // Public static method that returns the instance of the class, creating it if it doesn't exist
    public static MySingleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    public void doSomething() {
      System.out.println("Doing something...");
    }
}
```

The MySingleton class ensures that only one instance of itself will exist during the lifecycle of the application by making the constructor private, in other words, not allowing the class to be freely instantiated. The only way you can get an instance of this class is by calling the getInstance() method which will either instantiate the class if it hasn't been previously instantiated or by returning the already instance of the class.    

In Kotlin, creating singletons is much more simple. All you have to do is create an object instead of a class:    
```kotlin
object MySingleton {
    fun doSomething() {
        println("Doing something...")
    }
}
```

This object keyword tells Kotlin to create a single instance of MySingleton class. By decompiling Kotlin bytecode for the MySingleton object, we find that the Kotlin compiler generates all the necessary code to ensure the properties of a singleton class, without the explicit boilerplate:    
```kotlin
public final class MySingleton {
   public static final MySingleton INSTANCE;

   private MySingleton() {}

   static {
      INSTANCE = new MySingleton();
   }

    public final void doSomething() {
      System.out.println("Doing something...");
   }
}
```

Once again, Kotlin shows how its philosophy of blending functionality with simplicity, allows developers to focus more on solving business problems and less on boilerplate code.