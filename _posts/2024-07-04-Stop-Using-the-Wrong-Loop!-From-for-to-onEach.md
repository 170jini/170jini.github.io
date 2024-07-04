---
layout: post
title: "Stop Using the Wrong Loop! From for to onEach: Ultimate Guide to Kotlin Loops"
description: "Stop Using the Wrong Loop! From for to onEach: Ultimate Guide to Kotlin Loops"
summary: "Stop Using the Wrong Loop! From for to onEach: Ultimate Guide to Kotlin Loops"
tags: 
minute: 1
---
[Reference](https://chetan-garg36.medium.com/stop-using-the-wrong-loop-from-for-to-oneach-ultimate-guide-to-kotlin-loops-42dd25d6f3b3)    

Kotlin provides various ways to loop through data, each suitable for different use cases. Below are the primary looping constructs in Kotlin and my opinion on which one suits which cases.    

__*Warning!*__    
Don’t fight about imperative style or functional style looping! understand their merits and tradeoffs.    

__*When to Prefer Imperative Looping?*__    
1. Performance-Critical Code: Imperative loops can be more performant because they avoid the overhead of function calls and intermediate collections.    
2. Complex Logic: When the logic inside the loop is complex, involving multiple statements, and early exits (return, break, continue etc), imperative loops can be clearer and more straightforward.    
3. Mutable State: When the algorithm inherently involves changing the state over the course of the loop (e.g., updating a running total, managing an index) etc.    

__*When to Prefer Functional Looping:*__    
1. Readability and Expressiveness: Functional looping can be more concise and easier to read, especially for simple transformations and operations on collections.    
2. Immutability: Functional style often promotes immutability, which can lead to fewer bugs and easier reasoning about code.    
3. Parallelism and Lazy Evaluation: Functional constructs can be more easily parallelized and optimized by the compiler or runtime.    
4. Chainability: When you need to perform multiple operations in sequence, functional chaining can be more expressive and compact.    

__*So the point is :*__    
- Use Imperative Looping: When dealing with performance-critical sections, complex logic that benefits from explicit state management, or when the problem is inherently stateful.    
- Use Functional Looping: For simpler, more readable, and maintainable code, especially when working with immutable data structures and when performing chainable transformations.    

__*Iterating over range*__    
You need to iterate over a range of numbers.    

for Loop    
Use when you want to be explicit about your looping and you prefer the imperative style.    
```kotlin
for (i in 1..10) {
    println(i)
}
```

forEach function    
You prefer a functional style and want to apply a lambda function to each element in a collection. Useful when you are not being imperative.    
```kotlin
(1..10).forEach { it ->
  println(it)
}
```

__*Iterating over collections*__    
You need to iterate over elements in a collection.    

for Loop    
Use when you want to be explicit about your looping and you prefer the imperative style.    
```kotlin
val items = listOf("apple", "banana", "cherry")
for (item in items) {
    println(item)
}
```

forEach function    
You prefer a functional style and want to apply a lambda function to each element in a collection.    
```kotlin
val items = listOf("apple", "banana", "cherry")
items.forEach { item ->
    println(item)
}
```

__*Working with indexes of iterable/Collections*__    
You need an index from a collection / iterable.    
```kotlin
val items = listOf("apple", "banana", "cherry")
for (index in items.indices) {
    println("index $index")
}
```

__*Need both? item and index of iterable/Collections*__    

withIndex Loop    
You need both the index and the element from a collection, in a more idiomatic way.    
```kotlin
for ((index, item) in items.withIndex()) {
    println("Item at $index is $item")
}
```

forEachIndexed Loop    
You need both the index and the element from a collection in a functional style.    
```kotlin
items.forEachIndexed { index, item ->
    println("Item at $index is $item")
}
```

__*Manually Controlling iterations*__    
when you want to control iterations manually.    

while Loop    
You need to repeat an action until a condition becomes false, where the number of iterations is not known beforehand.    
```kotlin
var x = 0
while (x < 5) {
    println(x)
    x++
}
```

do-while Loop    
You need to ensure that the loop body is executed at least once before the condition is tested.    
```kotlin
var x = 0
do {
println(x)
x++
} while (x < 0)
```

__*Repeat some action a specific times*__    

repeat Loop    
You need to repeat an action a specific number of times. It is a more readable and concise way to handle fixed repetitions.    
```kotlin
repeat(5) {
    println("Hello")
}
```

__*Bonus :*__    

forEach function vs onEach Operator    
onEach and forEach are both functions that operate on collections, but they serve different purposes and have distinct behaviors.    

forEach    
- forEach is used to perform an action on each element of a collection, but the returns type is Unit. thus making it a terminal operation in the chains of operations.    
- It is mainly used for side effects, such as printing elements or modifying external states.    

Example using forEach:    
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
numbers.forEach { println(it) }
// Output: 1 2 3 4 5 (each number on a new line)
```
onEach    
- onEach is used to perform an action on each element of a collection but, unlike forEach, it returns the original collection after applying the action, thus you can chain operation over it.    
- Also, keep in mind it isn’t a transformation operator like map, the operation inside of onEach is just another side effect that doesn't update or transform the original collection in chain of operations.    
- Use it when you need to perform an action and then continue working with the collection (e.g., chaining further operations).    

Example using onEach:    
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val result = numbers
	.onEach { println(it) }
	.filter { it % 2 == 0 }
	.onEach { println(it) }
	
// Output during `onEach`: 1 2 3 4 5 (each number on a new line)
// Output after filter `onEach` : 2, 4 (each number on a new line)
```