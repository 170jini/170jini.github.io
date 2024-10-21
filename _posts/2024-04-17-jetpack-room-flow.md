---
layout: post
title: Room & Flow
description: Room & Flow
summary: Room & Flow
tags: 
minute: 1
---
[Link](https://medium.com/androiddevelopers/room-flow-273acffe5b57)

Coroutines support in Room has been increasing at every release: Room 2.1 added coroutines support for one-shot read / write operations and with Room 2.2 we now have support for observable reads with Flow enabling you to get notified of changes in your database.

#### Flow in action
Let’s say that we have a database of dogs, where the name is the primary key, therefore, we can’t have 2 dogs with the same name in the database.
```kotlin
@Entity
data class Dog (
    @PrimaryKey val name: String,
    val cuteness: Int,
    val barkingVolume: Int
)
```

To display a full list of dogs with all of their info we’d write a query like this in our DAO:
```kotlin
@Query("SELECT * FROM Dog")
fun getAllDogs(): List<Dog>
```

Because the barking volume of a dog can change over time and we want to make sure that our UI is up to date, then we want to get notified of every change that happens in the Dogs table: new dogs added, dogs removed or updated. To achieve this, we update the query to return Flow:
```kotlin
@Query("SELECT * FROM Dog")
fun getAllDogs(): Flow<List<Dog>>
```

Like this, whenever a dog in the database is updated, then the entire list of dogs is emitted again. For example, let’s say that we have the following data in the database:
```xml
(Frida, 11, 3)
(Bandit, 12, 5)
```

When we first call getAllDogs, our Flow will emit:
```xml
[(Frida, 11, 3), (Bandit, 12, 5)]
```

If Bandit gets excited and his bark volume is updated to 6: (Bandit, 12, 6), the Flow will emit again, with the entire content of the dogs table with the latest values:
```xml
[(Frida, 11, 3), (Bandit, 12, 6)]
```

Now let’s say that we can open a dog details in a new screen. Because we also want to ensure we always have the latest data on the dog and get updates in real time, we return a Flow:
```kotlin
@Query("SELECT * FROM Dog WHERE name = :name")
fun getDog(name: String): Flow<Dog>
```

Now, if we call getDog("Frida"), Flow will return one object: (Frida, 11, 3).

Whenever any changes are made to the table, independent of which row is changed, the query will be re-triggered and the Flow will emit again. So if Frida gets updated, we will receive the latest info.

However, this behaviour of the database also means that if we update an unrelated row, like Bandit, our Flow will emit again, with the same result: (Frida, 11, 3). Because SQLite database triggers only allow notifications at table level and not at row level, Room can’t know what exactly has changed in the table data, therefore it re-triggers the query defined in the DAO. In your code, use Flow operators like distinctUntilChanged, to ensure that you only get notified when the data you’re interested in has changed:
```kotlin
@Dao
abstract class DoggosDao {    
    @Query("SELECT * FROM Dog WHERE name = :name")
    abstract fun getDog(name: String): Flow<Dog>    
    fun getDogDistinctUntilChanged(name:String) =   
           getDog(name).distinctUntilChanged()
}
```

Start getting notified of the changes in your database by using observable reads with Flow! Together with other coroutines support added in Jetpack libraries like lifecycle-aware coroutine scopes, suspend lifecycle-aware coroutines or the transformation from Flow to LiveData, you can now use coroutines and Flow throughout your entire application.

To find out more about using Flow in your app, check out this post on the lessons learned while using Flow in the Android Dev Summit 2019 app.