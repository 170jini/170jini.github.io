---
layout: post
title: "Kotlin Tip #22: Use copy() to Modify Immutable Objects— 100 Kotlin Tips in 100 Days"
description: "Kotlin Tip #22: Use copy() to Modify Immutable Objects— 100 Kotlin Tips in 100 Days"
summary: "Kotlin Tip #22: Use copy() to Modify Immutable Objects— 100 Kotlin Tips in 100 Days"
tags: 
minute: 1
---
[Reference](https://medium.com/kotlin-with-raphael-de-lio/kotlin-tip-22-use-copy-to-modify-immutable-objects-100-kotlin-tips-in-100-days-f0151607a6a5)    

We've already discussed the benefits of data classes in this tip: . Data classes allow    

When defining classes in Kotlin, we have the option of defining their properties as immutable. Having immutable properties enhances the predictability and thread-safety of our code, making it less prone to errors and easier to maintain. (See: )    

However, sometimes we have to create a slightly modified copy of an existing object while keeping the original object unchanged. This is where the copy() function comes into play.    

Among all the utility functions automatically generated for Kotlin Data Classes (See: ) we can find the copy() function. This function allows for the creation of a new object with some properties modified, based on an existing object.    

Consider a data class User, defined as follows:    
```kotlin
data class User(val name: String, val age: Int)
```

If you want to create a new User instance based on an existing User but with a different age, you can use the copy() function:    
```kotlin
val originalUser = User(name = "Raphael De Lio", age = 30)
val updatedUser = originalUser.copy(age = 31)
```

This makes the task of creating a slightly modified copy of an existing object much easier. Especially when this object has several properties.    

The only thing to bear in mind is that the copy() function performs a shallow copy. This means that for properties that hold objects, the copied object will reference the same instances as the original object. Therefore, if you modify the mutable properties of the copied object, those changes will be reflected in the original object as well.    

Consider a data class with a mutable property:    
```kotlin
data class UserProfile(val name: String, val addresses: MutableList<String>)
```

Using copy() in this case:    
```kotlin
val originalProfile = UserProfile("Raphael De Lio", mutableListOf("123 Main St"))
val copiedProfile = originalProfile.copy()
```

If you add a new address to copiedProfile.addresses, it will also appear in originalProfile.addresses because both properties reference the same MutableList instance. Let’s try it:    
```kotlin
data class UserProfile(val name: String, val addresses: MutableList<String>)

fun main() {
    val originalProfile = UserProfile("Raphael De Lio", mutableListOf("123 Main St"))
	val copiedProfile = originalProfile.copy()
    
    copiedProfile.addresses.clear()
    
    println(originalProfile)
    println(copiedProfile)
}
```

If you run the code above, you will see that the address list from both variables have been cleared.    

To avoid unintended side effects, you would need to explicitly copy mutable properties as needed. For example:    
```kotlin
val copiedProfile = originalProfile.copy(addresses = originalProfile.addresses.toMutableList())
```

Let’s try it now:    
```kotlin
data class UserProfile(val name: String, val addresses: MutableList<String>)

fun main() {
    val originalProfile = UserProfile("Raphael De Lio", mutableListOf("123 Main St"))
	val copiedProfile = originalProfile.copy(addresses = originalProfile.addresses.toMutableList())    
    
    copiedProfile.addresses.clear()
    
    println(originalProfile)
    println(copiedProfile)
}
```

In this example, copiedProfile has its own independent address list. Changes to the address list in copiedProfile will not affect originalProfile, achieving true immutability.